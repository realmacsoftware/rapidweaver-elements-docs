---
description: Generate repeating layouts with user-managed dropzones from collections
---

# Collection-Driven Dropzones

This is the pattern behind almost every tabbed, accordion, or slider-style component in Elements: a [collection](../component/collections/README.md) defines *how many* regions exist, a [`@dropzone`](../component/language/dropzone.md) inside an [`@each`](../component/language/each.md) loop gives each region its own child-component area, and your hooks stitch the iterations together with ids and ARIA attributes. The user adds a tab in the inspector — and a whole new panel appears in the editor, ready to receive dropped components. This guide walks the pattern end to end, from collection schema to accessible markup.

{% hint style="success" %}
This guide dissects the **Tabs** (`com.realmacsoftware.tabs`) and **Table** (`com.realmacsoftware.table`) components from the open-source [Core Pack](../development-resources/open-source-components.md). Open their source alongside this page.
{% endhint %}

## From Static Dropzones to Loops

A static dropzone is a fixed hole in your template — you decide at design time that your component has a `"header"` area and a `"content"` area, and every instance of the component has exactly those two. The [`@dropzone` reference](../component/language/dropzone.md) covers this form, including its `title` and `horizontal` parameters and a short section on dropzones inside loops.

Collection-driven dropzones invert the ownership. Instead of you deciding how many content areas exist, the *user* decides — by adding, removing, and reordering items in a collection panel in the inspector. Your template declares the dropzone once, inside a loop over the collection, and Elements creates one real dropzone per iteration. Three pieces cooperate:

1. **The collection** (`collections/{name}/`) defines the repeatable item and its per-item fields — a tab's title, a slide's caption, a column's width.
2. **The hooks file** reads the collection from `rw.collections`, computes anything the template shouldn't have to (active index, per-item ids, precomputed booleans), and passes the processed array to templates with `rw.setProps`.
3. **The template** loops the array with `@each` and places `@dropzone` (and any ARIA wiring) inside the loop body.

## Worked Example: The Core Tabs Component

### The Collection Defines How Many Panels Exist

The Tabs component's collection lives at `collections/tabs/` and consists of three small JSON files. First, `info.json` gives the collection an identity:

```json
// collections/tabs/info.json
{
    "identifier": "com.realmacsoftware.tabs.collections.tabs",
    "title": "Tabs"
}
```

Second, `properties.json` defines the inspector fields each *individual tab* carries — here just a title and an optional SVG icon:

```json
// collections/tabs/properties.json
{
    "groups": [
        {
            "title": "Tab",
            "properties": [
                {
                    "title": "Title",
                    "property": "title",
                    "responsive": false,
                    "text": { "default": "Tab" }
                },
                {
                    "title": "Icon",
                    "property": "icon",
                    "responsive": false,
                    "resource": { "accepts": "svg" }
                }
            ]
        }
    ]
}
```

Third, `defaults.json` seeds every freshly added Tabs component with three starter tabs, so users see a working tabbed layout immediately instead of an empty shell:

```json
// collections/tabs/defaults.json
{
    "items": [
        { "title": "Tab 1" },
        { "title": "Tab 2" },
        { "title": "Tab 3" }
    ]
}
```

Finally, the component's main `properties.json` registers the collection with a `collection` control that references the identifier above, under the property name `tabs` — the name you read it back with in hooks and templates. See [Collections in properties.json](../component/collections/collections-in-properties.json.md) for the registration syntax.

Nothing in these files mentions dropzones. The collection's only job is to model the repeatable item; the count of items *is* the count of panels, and that connection is made in the next two files. See [Collections](../component/collections/README.md) for the full schema reference.

### Hooks Prepare One Item Per Iteration

The hooks file turns the raw collection into a template-ready array. Here is the relevant excerpt from `hooks.source.js`:

```javascript
// hooks.source.js (excerpt)
const transformHook = (rw) => {
    // …around 90 styling-related props destructured from rw.props elided,
    // including defaultActiveTab, editorActiveTab, and showAboveContent used below…

    const { mode } = rw.project;
    const { id } = rw.node;
    const { tabs } = rw.collections;
    const edit = mode === "edit";

    // Determine which tab to show as active in editor mode
    const activeTabIndex = edit
        ? Math.max(0, Math.min((parseInt(editorActiveTab) || 1) - 1, (tabs?.length || 1) - 1))
        : Math.max(0, Math.min((parseInt(defaultActiveTab) || 1) - 1, (tabs?.length || 1) - 1));

    // …Tailwind class computation for buttons, titles, and icons elided…

    // Process tabs from collection
    const tabItems = tabs?.map((tab, index) => {
        const isActive = index === activeTabIndex;
        // …per-state class selection and SVG icon processing elided…

        return {
            id: `tab-${id}-${index}`,
            title: tab.title || `Tab ${index + 1}`,
            index: index,
            isActive,
            // Pre-computed for template: hide panel in editor if not active
            hideInEditor: edit && !isActive,
        };
    }) || [];

    // …classes object and rw.setRootElement call elided…

    rw.setProps({
        id,
        classes,
        tabItems,
        edit,
        editorActiveTabIndex: activeTabIndex,
        showAboveContent: showAboveContent === true || showAboveContent === "true",
    });
};
```

Three decisions here carry the whole pattern:

* **The active index is clamped, not trusted.** `defaultActiveTab` is a 1-based number the user types into the inspector, so the hook converts it to 0-based and clamps it to the actual number of tabs — deleting tabs can otherwise leave the "active" index pointing at nothing. In edit mode a separate `editorActiveTab` property drives the preview instead, so authors can flip between panels without changing what visitors see.
* **Every item gets a stable identity.** Each processed item carries its `index` and an id derived from the component's node id (`tab-${id}-${index}`). The node id keeps ids unique when two Tabs components share a page; the index keys everything else — Alpine state, ARIA relationships, panel visibility.
* **Booleans are precomputed.** `hideInEditor` folds `edit && !isActive` into a single flag because `@if` in templates takes exactly one condition — no `&&` or `==`. Whenever a template needs a compound test, compute it here.

### The Template Renders a Dropzone Per Panel

The template loops `tabItems` twice over the same data: once to build the row of tab buttons, once to build the panels. Each panel iteration contains the `@dropzone`:

```html
<!-- templates/index.html (excerpt) -->
<!-- Tab List -->
<div class="{{classes.tabList}}" role="tablist" aria-label="Tabs">
    @each(tab in tabItems)
        <button
            @if(!edit)
                x-bind="tabButton"
                :class="activeTab === {{ tab.index }} ? '{{classes.tabButtonActive}}' : '{{classes.tabButtonInactive}}'"
            @endif
            class="{{tab.buttonClass}}"
            role="tab"
            :id="'tab-btn-' + '{{id}}' + '-' + {{ tab.index }}"
            :aria-selected="activeTab === {{ tab.index }}"
            :aria-controls="'tab-panel-' + '{{id}}' + '-' + {{ tab.index }}"
            :tabindex="activeTab === {{ tab.index }} ? 0 : -1"
            data-tab-index="{{ tab.index }}"
        >
            <!-- …icon and title spans elided… -->
        </button>
    @endeach
</div>

<!-- Tab Panels -->
<div class="{{classes.tabPanelsWrapper}}">
    @each(tab in tabItems)
    <div
        @if(!edit)
        x-bind="tabPanel"
        x-show="activeTab === {{ tab.index }}"
        x-cloak
        @endif
        @if(tab.hideInEditor)
        style="display: none;"
        @endif
        class="{{classes.tabPanel}}"
        role="tabpanel"
        :id="'tab-panel-' + '{{id}}' + '-' + {{ tab.index }}"
        :aria-labelledby="'tab-btn-' + '{{id}}' + '-' + {{ tab.index }}"
        data-tab-panel="{{ tab.index }}"
    >
        @dropzone("tabContent", title: "Below Content")
    </div>
    @endeach
</div>
```

Walk the stitching. Every button computes an id of `tab-btn-{componentId}-{index}` and points its `aria-controls` at `tab-panel-{componentId}-{index}`; every panel computes the matching `id` and points `aria-labelledby` back at the button. Because both loops iterate the same `tabItems` array, iteration *n* of the button loop and iteration *n* of the panel loop always agree — the hook's per-item `index` is the thread that ties the two passes together. Screen readers get a fully wired `tablist`/`tab`/`tabpanel` structure, and the shared Alpine behaviour (registered once in `templates/alpine.html`) drives `activeTab` from clicks and arrow keys.

Notice what `@dropzone("tabContent", …)` does *not* do: it never mentions the index. The name is the same static literal in every iteration, yet each tab gets its own independent dropzone with its own child components. That is Elements' job, not yours — which brings us to the rules.

## Rules and Gotchas

* **Dropzone names are static literals.** You cannot write `@dropzone("panel-{{tab.index}}")` or interpolate any template value into the name or title. Declare the name once, as plain text.
* **Elements uniquifies per iteration.** One `@dropzone("tabContent")` declaration inside `@each` becomes one real, independent dropzone per iteration — each with its own dropped children, persisted against that collection item. This works through nested loops too: the Table component's single `@dropzone("cell")` sits inside a rows loop *and* a columns loop, producing a distinct dropzone for every row–column pair. Distinct *regions* still need distinct names, though — Tabs uses `"tabAboveContent"` for its optional above-tab-list panels and `"tabContent"` for the main panels.
* **Loop metadata is available when you need it.** Inside `@each`, the template language provides `::index`, `::isFirst`, and `::isLast` on the loop variable (for example `tab::index`) — see the [`@each` reference](../component/language/each.md). Tabs doesn't use them because its hook already bakes `index` into each item; prefer that approach when the index feeds many expressions, and the `::` variables for one-off cases like first/last styling.
* **Deleting an item deletes its dropzones.** When the user removes a collection item, the dropzones generated for that iteration disappear — along with every child component the user dropped into them.

{% hint style="warning" %}
Content inside a per-iteration dropzone belongs to that collection item. Removing the item from the collection panel removes the dropped child components with it, so make your item titles descriptive enough that users can tell which panel they are about to delete.
{% endhint %}

## Choosing Dropzone or Content Per Item

Sometimes a region shouldn't *always* be a dropzone. The core Table component lets users decide, column by column, whether cells hold plain editable text or a full dropzone. The choice is a `segmented` control in the columns collection's `properties.json` — a `cellMode` property whose two values are `"text"` (the default) and `"dropzone"`. The hook converts that string into booleans the template can test directly — again because `@if` takes a single condition, never a comparison:

```javascript
// hooks.source.js (excerpt)
// Build rows array from rowCount
const count = Math.max(1, parseInt(rowCount) || 3);
const rows = Array.from({ length: count }, (_, i) => ({ index: i }));

// Process columns to include per-column classes (respects collection order)
const processedColumns = columns?.map((col, index) => {
    const isDropzone = col.cellMode === "dropzone";
    // …sortable and hidden flags elided…

    return {
        ...col,
        index,
        isDropzone,
        isText: !isDropzone,
        // …width, alignment, and CSS class fields elided…
    };
}) || [];
```

Note the two different axes: columns come from a collection, but rows are just an array the hook builds from a `rowCount` number property. `@each` doesn't care where the array came from — a collection, a hook-built array, or a resource folder all loop the same way.

The template then switches per cell:

```html
<!-- templates/index.php (excerpt) -->
<tbody class="{{classes.tbody}}">
    @each(row in rows)
    <tr class="{{classes.tr}}"
        @if(!edit)
        x-ref="row{{row.index}}"
        x-show="isRowVisible($el)"
        @endif
    >
        @each(column in columns)
        <td class="{{classes.td}} {{column.widthClass}} {{column.bodyAlignmentClass}} {{column.hiddenClass}} {{column.extraClasses}}">
            @if(column.isDropzone)
                @dropzone("cell", title: "Cell")
            @else
                @text("cell", default: "Cell")
            @endif
        </td>
        @endeach
    </tr>
    @endeach
</tbody>
```

A text-mode column renders an inline-editable [`@text`](../component/language/text.md) region in every cell — fast to fill in, impossible to break the layout with. Flipping the column's Cell Mode to Dropzone swaps every cell in that column to a dropzone that accepts buttons, images, or any other component. The per-item switch means one Table serves both a simple pricing grid and a feature-comparison matrix with rich cells — without two components or a global either/or setting.

## Paired Dropzones Per Iteration

A collection item can own *more than one* dropzone. A common shape — used by slider-style components that pair each slide with a custom thumbnail — is to loop the same collection twice, declaring a different dropzone name in each pass. Here is a generic card deck (`com.example.cardDeck`) that gives every card a user-composed face and a matching detail panel:

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { id } = rw.node;
    const { mode } = rw.project;
    const { cards } = rw.collections;
    const edit = mode === "edit";

    const cardItems = (cards || []).map((card, index) => ({
        title: card.title || `Card ${index + 1}`,
        index,
        faceId: `card-face-${id}-${index}`,
        detailId: `card-detail-${id}-${index}`,
    }));

    rw.setProps({ id, edit, cardItems });
};
```

```html
<!-- templates/index.html -->
<div x-data="{ activeCard: 0 }">
    <!-- Pass one: the clickable card faces -->
    <div class="flex flex-wrap gap-4" role="tablist" aria-label="Cards">
        @each(card in cardItems)
            <div
                role="tab"
                id="{{card.faceId}}"
                aria-controls="{{card.detailId}}"
                :aria-selected="activeCard === {{card.index}}"
                :tabindex="activeCard === {{card.index}} ? 0 : -1"
                @click="activeCard = {{card.index}}"
            >
                @dropzone("cardFace", title: "Card Face")
            </div>
        @endeach
    </div>

    <!-- Pass two: the matching detail panels -->
    @each(card in cardItems)
        <section
            role="tabpanel"
            id="{{card.detailId}}"
            aria-labelledby="{{card.faceId}}"
            @if(!edit)
            x-show="activeCard === {{card.index}}"
            x-cloak
            @endif
        >
            @dropzone("cardDetail", title: "Card Detail")
        </section>
    @endeach
</div>
```

Each collection item now owns two dropzones — `"cardFace"` from the first pass and `"cardDetail"` from the second — and the hook-generated `faceId`/`detailId` pair wires them together with `aria-controls`/`aria-labelledby`, exactly as Tabs does. Because the hook precomputes the full id strings, the template can use plain `id="{{card.faceId}}"` attributes instead of Alpine-bound expressions. In edit mode the `x-show` is omitted, so every detail panel stays visible and users can drop content into each one; the [edit-mode guide](edit-mode-experience.md) covers refinements like previewing a single active panel.

Adding one card in the inspector creates both of its dropzones at once. Deleting it removes both — and everything inside them.

## Nested Item Data

Collection items aren't limited to flat fields — an item can carry list-like data that your template renders with a nested `@each`. Since collection schemas define single values per property, the idiomatic trick is a multi-line `textArea` that hooks split into an array. Here is a generic pricing table (`com.example.pricing`) whose tiers each carry a feature list:

```json
// collections/tiers/properties.json
{
    "groups": [
        {
            "title": "Tier",
            "properties": [
                { "title": "Name", "property": "name", "responsive": false, "text": { "default": "Starter" } },
                { "title": "Price", "property": "price", "responsive": false, "text": { "default": "$9" } },
                {
                    "title": "Features",
                    "property": "features",
                    "responsive": false,
                    "textArea": { "default": "One project\nEmail support" }
                }
            ]
        }
    ]
}
```

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { tiers } = rw.collections;

    const tierItems = (tiers || []).map((tier, index) => ({
        ...tier,
        index,
        featureItems: (tier.features || "")
            .split("\n")
            .map((line) => ({ label: line.trim() }))
            .filter((feature) => feature.label.length > 0),
    }));

    rw.setProps({ tierItems });
};
```

```html
<!-- templates/index.html -->
<div class="grid gap-6 md:grid-cols-3">
    @each(tier in tierItems)
        <section class="pricing-card">
            <h3>{{tier.name}}</h3>
            <p class="price">{{tier.price}}</p>
            <ul>
                @each(feature in tier.featureItems)
                    <li>{{feature.label}}</li>
                @endeach
            </ul>
            @dropzone("tierAction", title: "Call to Action")
        </section>
    @endeach
</div>
```

The nested loop follows the same shape as the [`@each` reference's](../component/language/each.md) nested-loops example: the inner `@each` iterates an array carried by the outer loop's item, and each level gets its own descriptive variable name. The hook maps each line to an object with a `label` field so the template reads it with the same dot notation as every other collection field. Users edit the feature list as plain lines of text in the inspector — one line per feature, no markup to learn — while the `"tierAction"` dropzone still gives each tier a fully composable button area. Structured where it pays off, free-form where it doesn't.

## Related Documentation

* [@dropzone](../component/language/dropzone.md)
* [@each](../component/language/each.md)
* [Collections](../component/collections/README.md)
* [Accessing Data in Templates](../component/collections/accessing-data-in-templates.md)
* [Designing the Edit-Mode Experience](edit-mode-experience.md)
* [Interactive Components with Alpine.js](interactive-components-with-alpine.md)
