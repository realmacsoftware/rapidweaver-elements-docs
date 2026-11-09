---
description: Make components feel great on the editing canvas with placeholders, preview data, and editor styles
---

# Designing the Edit-Mode Experience

Your component will spend most of its life on the editing canvas. Users drop it in empty, click into it, rearrange it, and stare at it while making decisions — long before a visitor ever sees the published page. A component that renders perfectly when published but sits blank, broken, or booby-trapped in the editor feels unfinished, no matter how good the shipped output is. The techniques for a great edit-mode experience are scattered across the reference docs; this guide pulls them into one place.

{% hint style="success" %}
This guide dissects the **Table** (`com.realmacsoftware.table`), **Tabs** (`com.realmacsoftware.tabs`), and **Gallery** (`com.realmacsoftware.gallery`) components from the open-source [Core Pack](../development-resources/open-source-components.md). Open their source alongside this page.
{% endhint %}

## Detecting the Mode

Everything in this guide starts from one question: *am I on the canvas right now?* You can answer it in both places your code runs.

In `hooks.js`, read [`rw.project.mode`](../component/hooks.js/available-data/rw.project.md#edit-vs-preview-mode) — it's `"edit"` on the canvas and `"preview"` otherwise. Every core component that cares about mode computes a boolean once, near the top of its hook, and reuses it everywhere. Here is Table's version:

```javascript
// com.realmacsoftware.table/hooks.source.js
const transformHook = (rw) => {
    // …
    const { mode } = rw.project;
    const edit = mode === "edit";
    // …
    rw.setProps({
        // …
        edit,
    });
};

exports.transformHook = transformHook;
```

In templates, you don't even need the hook: Elements provides built-in [`edit` and `preview` variables](../component/language/if.md#editpreview-mode-detection), so `@if(edit)`, `@if(!edit)`, and the three-way split all work out of the box:

```html
@if(edit)
    Visible in Edit mode (inside Elements)
@elseif(preview)
    Visible in local preview (in Safari).
@else
    Visible when Published.
@endif
```

Remember that template `@if` takes exactly **one** condition — no `&&`, `||`, or comparisons. When a decision involves mode *and* something else (Gallery's lightbox below is a good example), combine them in `hooks.js` and pass a single boolean to the template. See [Combining Conditions](../component/language/if.md#combining-conditions).

## Empty-State Placeholders

The very first thing a user sees after dropping your component on the canvas is your empty state. If that's a zero-height blank box, they'll assume the component is broken. Gallery handles this by computing a single `hasResources` boolean in its hook:

```javascript
// com.realmacsoftware.gallery/hooks.source.js
const transformHook = (rw) => {
    // …
    const hasResources = resources?.resources?.length > 0;
    // …
};

exports.transformHook = transformHook;
```

…and branching its entire main template on it. When the gallery is empty, users don't see nothing — they see a generously sized, dashed-border drop target that tells them exactly what to do next:

```html
<!-- com.realmacsoftware.gallery/templates/index.html -->
@if(!hasResources)
<div
    rwResourceDropZone="resources"
    class="col-span-full w-full h-64 flex flex-col items-center justify-center border-2 border-dashed border-gray-300 rounded-xl bg-gray-50 hover:bg-gray-100 transition cursor-pointer text-center px-4 py-6"
>
    <!-- … folder icon SVG … -->
    <p class="text-lg font-medium text-gray-700">
        Drag & drop a folder of resources
    </p>
    <p class="text-sm text-gray-400">or add them via the component inspector</p>
</div>
@else
<div class="{{classes.wrapper}}" x-data>
    @each(image in resources) @include("thumbnail") @endeach
</div>
@endif @includeIf(includeLightbox, template: "lightbox")
```

Three details worth stealing:

* **The placeholder is keyed to content, not mode.** It appears whenever the gallery is empty, so a user who previews before adding images still gets guidance instead of a void.
* **The placeholder is functional.** The `rwResourceDropZone="resources"` attribute (visible in the Gallery source) makes the placeholder itself accept the drop, so the instruction and the target are the same element.
* **It names both paths.** Drag and drop *or* the inspector — whichever workflow the user prefers, the placeholder covers it.

For collection-driven components, the equivalent pattern is a **placeholder item**: when the collection is empty, fall back to a hard-coded sample entry so the component still renders its real layout. The core Audio Playlist does exactly this with a fallback "first track" — see the [full example in Data Collections in hooks.js](../component/collections/data-collections-in-hooks.js.md#full-example-audio-playlist) rather than duplicating it here.

## Preview Datasets

Placeholders cover "no content yet". Data-driven components have a harder problem: the *real* content lives somewhere the editor can't reach. Table's CSV mode is the canonical case — on the published site the data comes from a CSV file or remote URL, fetched and parsed by PHP at request time. None of that machinery exists on the canvas, so in edit mode Table fabricates a realistic sample dataset in its hook instead:

```javascript
// com.realmacsoftware.table/hooks.source.js
const transformHook = (rw) => {
    // …
    // Example data for edit mode preview when using CSV sources
    const previewColumnCount = Math.max(processedColumns.length, 1);
    const previewColumnLabel = (index) => {
        if (index < 26) {
            return `column_${String.fromCharCode(97 + index)}`;
        }
        return `column_${index + 1}`;
    };

    const headerRow = Array.from({ length: previewColumnCount }, (_, index) => ({
        label: previewColumnLabel(index),
    }));
    const bodyRows = Array.from({ length: 5 }, (_, rowIndex) => ({
        cells: Array.from({ length: previewColumnCount }, (_, colIndex) => ({
            value: `row ${rowIndex + 1}, cell ${colIndex + 1}`,
        })),
    }));
    // …
    rw.setProps({
        // …
        exampleShowHeader,
        examplePreviewHeaders,
        examplePreviewRows,
    });
};

exports.transformHook = transformHook;
```

The template's CSV branch then splits on `edit`: the canvas renders the sample rows through the *same* classes the real table will use, followed by an honest caption; everything after `@else` is the live PHP + Alpine implementation that only ever runs on the published site.

```html
<!-- com.realmacsoftware.table/templates/index.php (inside the CSV branch) -->
@if(edit)
<div>
    <table class="{{classes.table}}">
        <!-- … optional example header row … -->
        <tbody>
            @each(row in examplePreviewRows)
            <tr class="{{classes.tr}}">
                @each(cell in row.cells)
                <td class="{{classes.td}} {{cell.widthClass}} {{cell.alignmentClass}} {{cell.hiddenClass}} {{cell.extraClasses}}">
                    {{cell.value}}
                </td>
                @endeach
            </tr>
            @endeach
        </tbody>
    </table>
    <p style="opacity: 0.35; font-size: 0.85em; margin-top: 0.5rem; text-align: center;">
        @if(isCSVFile)
        Example data &mdash; CSV file will be loaded on the published site.
        @elseif(isCSVUrl)
        Example data &mdash; CSV URL will be loaded on the published site.
        @endif
    </p>
</div>

@else
<!-- … the live table: PHP fetches and parses the CSV at request time … -->
@endif
```

Two rules make a preview dataset trustworthy rather than confusing:

1. **Label it.** The dimmed "Example data" caption tells users this isn't their CSV, and where the real data will come from.
2. **Style it for real.** The sample cells run through the user's actual column configuration — widths, alignment, hidden columns, custom classes — so styling decisions made against fake data survive contact with real data.

## Editor-Only CSS

Sometimes the canvas needs styling the published page must never see. Any `.css` file at the root of `templates/` runs through the template engine (see [CSS Templates](../component/templates/css-templates.md)), which means it can use `@if(edit)` like any other template. Wrap the whole file in it and the file contributes **zero bytes** to the published page. Tabs uses exactly this to show only the panel currently being edited:

```css
/* com.realmacsoftware.tabs/templates/editor-ui.css */
@if (edit)

/* … */

/* Tab panels in editor - show the one being edited */
[role="tabpanel"] {
    display: none;
}

/* The active panel should be visible */
[role="tabpanel"][data-tab-panel="{{editorActiveTabIndex}}"] {
    display: block;
}

@endif
```

`{{editorActiveTabIndex}}` is computed in `hooks.js` from an inspector property, so the stylesheet re-targets a different panel every time the user picks a different tab to edit — no page JavaScript involved. Ordinary component scripts, Alpine factories, and pack `bodyEnd` loaders still do not run on the canvas. If a scene must actually animate while the user edits (Three.js and similar), use the [`rwlivepreview` contract](editor-live-preview.md) instead of relying on those scripts.

Navbar's `templates/editor.css` shows the minimal end of the same idea: a single rule fixing the width of `[data-rwx-droparea]` elements, the drop areas Elements injects into the canvas. Those elements only exist in the editor, so the rule is inert when published — but wrapping editor CSS in `@if(edit)` is still the better habit, because it removes the text from the published output entirely instead of merely leaving it unmatched.

## Gating Heavy Behaviour on the Canvas

The canvas is not a browser tab you control. It re-renders constantly as the user edits, and anything that autoplays, observes, animates, or floats above the page becomes noise at best and a click-trap at worst. The core components are aggressive about switching this machinery off in edit mode.

Gallery's lightbox is the clearest example. Rendering a fixed, full-screen overlay on the canvas would be hostile, so the hook decides whether to include the lightbox template at all — and combines the mode check with a user-facing opt-in switch, precisely because template `@if` couldn't express that combination itself:

```javascript
// com.realmacsoftware.gallery/hooks.source.js
const transformHook = (rw) => {
    // …
    rw.setProps({
        // …
        edit: rw.project.mode === "edit",
        includeLightbox: lightboxPreview || rw.project.mode !== "edit",
        // …
    });
};

exports.transformHook = transformHook;
```

The template consumes the single boolean: `@includeIf(includeLightbox, template: "lightbox")`. By default the lightbox simply doesn't exist on the canvas; flip the Lightbox Preview switch in the inspector and it appears, so users can still style it. **Gate by default, offer an opt-in** is the pattern to copy for any overlay, animation, or effect a user might occasionally need to see while editing.

Modal shows the template-level counterpart with `x-cloak`. Alpine removes `x-cloak` attributes when it initialises — but Alpine never initialises on the canvas, so an unconditionally cloaked element would be invisible there forever. Modal only cloaks outside the editor:

```html
<!-- com.realmacsoftware.modal/templates/index.html -->
@portal("bodyEnd")
<div
    x-dialog
    @if(!edit)
    x-cloak
    @endif
    x-data="{
        open: false,
        stopAllMedia() { /* … pause videos, audio, and iframes … */ }
    }"
    x-init="$watch('open', value => { if (!value) { stopAllMedia(); } })"
    @open-modal.window="(e) => { open = e.detail.id === '{{id}}' }"
    x-model="open"
    class="{{classes.dialog}}"
    data-modal-id="{{id}}"
>
    <!-- … overlay and panel markup, ending in the "content" dropzone … -->
</div>
@endportal
```

On the published page, `x-cloak` prevents a flash of un-styled modal before Alpine wakes up; on the canvas, omitting it keeps the dialog markup renderable so its content stays editable (more on that below). Table applies the same discipline to plain interactivity: its wrapper only gets `x-data="elementsTable(…)"` outside edit mode, and the search input renders `disabled` on the canvas — visible, styleable, but inert.

## Keeping Hidden Content Editable

Show/hide components have a built-in edit-mode conflict: at runtime, most of their content is *supposed* to be invisible, but on the canvas every dropzone must stay reachable or users can't fill it. The core answer is to run visibility through two completely separate mechanisms — Alpine at runtime, precomputed inline styles in the editor.

Tabs decides which panel is "active" from a different source per mode: the visitor-facing `defaultActiveTab` property at runtime, but a dedicated `editorActiveTab` inspector property on the canvas, so users choose which tab they're editing. The hook folds that into a per-panel boolean:

```javascript
// com.realmacsoftware.tabs/hooks.source.js
const transformHook = (rw) => {
    // …
    // Determine which tab to show as active in editor mode
    const activeTabIndex = edit
        ? Math.max(0, Math.min((parseInt(editorActiveTab) || 1) - 1, (tabs?.length || 1) - 1))
        : Math.max(0, Math.min((parseInt(defaultActiveTab) || 1) - 1, (tabs?.length || 1) - 1));
    // …
    const tabItems = tabs?.map((tab, index) => {
        const isActive = index === activeTabIndex;
        return {
            // …
            // Pre-computed for template: hide panel in editor if not active
            hideInEditor: edit && !isActive,
        };
    }) || [];
    // …
};

exports.transformHook = transformHook;
```

The panel markup then carries both mechanisms side by side — Alpine bindings that only exist outside edit mode, and a plain `display: none` that only appears in the editor:

```html
<!-- com.realmacsoftware.tabs/templates/index.html -->
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
```

Every panel is always in the markup; which one is visible is an editor decision on the canvas and an Alpine decision at runtime. Accordion is the same idea inverted: its collapsible region starts `display: none` on the published page (Alpine's `x-collapse` opens it), but in edit mode the inline style is skipped so the panel sits open and its dropzone is always reachable:

```html
<!-- com.realmacsoftware.accordion/templates/index.html -->
<div
    x-bind="content"
    x-collapse
    @if(!edit)
    style="display: none;"
    @endif
    :id="'accordion-content-' + '{{id}}'"
    role="region"
    :aria-hidden="(!open).toString()"
    :aria-labelledby="'accordion-header-' + '{{id}}'"
    class="{{classes.content}}"
>
    @dropzone("content", title: "Content")
</div>
```

Modal rounds out the pattern in its hook: the dialog's classes include `hidden` on the canvas unless the user enables a show-in-edit switch, and the full-screen overlay always gets `pointer-events-none` in edit mode so it can never swallow canvas clicks even while visible.

{% hint style="success" %}
**Ship-quality checklist** — run through this before releasing a component:

* [ ] Mode logic is computed once in `hooks.js` (`const edit = rw.project.mode === "edit"`) and passed down as booleans — never faked with multi-condition template `@if`.
* [ ] An empty component renders a helpful, generously sized placeholder — not a blank box — and the placeholder says exactly what to do next.
* [ ] Components fed by external data show labelled, realistically styled sample data on the canvas.
* [ ] Editor-only CSS lives in a `templates/*.css` file wrapped entirely in `@if(edit)`, contributing nothing to the published page.
* [ ] No overlays, autoplay, observers, or Alpine initialisation run on the canvas by default.
* [ ] Interactive states users need to style (lightboxes, modals) are reachable in edit mode via an opt-in inspector switch.
* [ ] Every dropzone is reachable on the canvas — hidden panels use an editor-active property instead of staying collapsed.
* [ ] `x-cloak` and runtime `display: none` styles are emitted only inside `@if(!edit)`.
{% endhint %}

## Related Documentation

* [rw.project](../component/hooks.js/available-data/rw.project.md) — the `mode` property and other project data
* [@if](../component/language/if.md) — built-in `edit`/`preview` variables and combining conditions
* [CSS Templates](../component/templates/css-templates.md) — how `templates/*.css` files are processed
* [Data Collections in hooks.js](../component/collections/data-collections-in-hooks.js.md) — placeholder items for empty collections
* [Collection-Driven Dropzones](collection-driven-dropzones.md)
* [Modals, Overlays & Portals](modals-overlays-and-portals.md)
