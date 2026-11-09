---
description: Build navigation components with rw.pages and recursive includes
---

# Navigation & Recursive Templates

Navigation components have a problem no other component family shares: their content is a tree of unknown depth. A user's project might be five flat pages, or a folder inside a folder inside a folder. Your hook receives that tree as [`rw.pages`](../component/hooks.js/available-data/rw.pages.md), and your templates have to turn it into markup without knowing in advance how deep it goes. The core answer is a technique this guide covers in full: a template that `@include`s **itself**, once per child level, until the tree runs out.

{% hint style="success" %}
This guide dissects the **Tree** (`com.realmacsoftware.navTree`) and **Menu** (`com.realmacsoftware.navbar`) components from the open-source [Core Pack](../development-resources/open-source-components.md). Open their source alongside this page.
{% endhint %}

## The Page Tree

`rw.pages` is an array of page objects mirroring the project's page list. Each object carries identity (`title`, `url`, `description`), type flags (`isPage`, `isFolder`, `isLink`), state (`isActive`, `hasActiveChild`, `isDraft`), menu metadata (`displayInMenu`, `openInNewWindow`), depth info (`navLevel`, `pageDepth`), and — crucially — its children: `hasPages` plus a nested `pages` array of the same shape. The full field reference lives in [rw.pages](../component/hooks.js/available-data/rw.pages.md); everything below uses only those documented fields.

Because children are the same shape as parents, every real traversal is recursive. Tree does its entire preparation in one recursive pass — filtering, ID generation, depth limits, and active-state rollup in a single function:

```javascript
// com.realmacsoftware.navTree/hooks.source.js
// Efficient recursive traversal: include node only if it should be shown
const buildPages = (pages, parentPath = "", relativeLevel = 0) => {
    const result = [];
    if (!Array.isArray(pages) || pages.length === 0) return result;

    // Check if we've reached the maximum depth limit
    const hasReachedMaxDepth =
        maxLevelsDepth === "manual" && maxLevels > 0 && relativeLevel >= maxLevels;

    for (let i = 0; i < pages.length; i += 1) {
        const page = pages[i];
        if (!(page.displayInMenu && !page.isDraft)) continue;

        const slug = slugify(page.title);
        const id = parentPath ? parentPath + "-" + slug : slug;

        // Only build children if we haven't reached the maximum depth
        const children = hasReachedMaxDepth
            ? []
            : buildPages(page.pages || [], id, relativeLevel + 1);

        const hasPages = children.length > 0;
        const hasActiveChild =
            hasPages &&
            children.some((c) => c.isActive || c.hasActiveChild);

        const processedPage = {
            ...page,
            id,
            pages: children,
            hasPages,
            hasActiveChild,
            isTopLevel: relativeLevel === 0,
            isSecondLevel: relativeLevel === 1,
            isThirdLevel: relativeLevel >= 2,
            showPageIcon: pageIconDisplay && relativeLevel === 0,
        };

        if (processedPage.isActive || hasActiveChild) {
            openPages.push(id);
        }

        result.push(processedPage);
    }

    return result;
};
```

Five decisions in this function are worth stealing for any nav component:

* **Filter as you walk.** `page.displayInMenu && !page.isDraft` drops drafts and pages excluded from the menu at every level, so the template never needs to know those pages exist.
* **Rebuild derived fields after filtering.** `hasPages` and `hasActiveChild` are recomputed from the *filtered* children — if a folder's only child was a draft, the folder correctly renders as a leaf.
* **Give every node a stable ID.** Slugified titles joined down the parent path (`docs-getting-started`) give the template something to hand to Alpine for expand/collapse state and `localStorage` persistence.
* **Enforce depth in the hook, not the template.** When the user picks a manual depth limit (the inspector's `maxLevelsDepth`/`maxLevels` properties), children beyond the limit are simply never built — the template needs no depth logic at all.
* **Precompute level booleans.** `isTopLevel`/`isSecondLevel`/`isThirdLevel` become single-condition `@if` tests in the template, which matters because template `@if` accepts exactly one condition.

Around this core, the hook also scopes *which* subtree to walk: a `wantedPages` inspector property selects the whole project (`rw.pages`), the active page's children (found with a recursive `findActivePage`), or a manually chosen folder (found with a recursive `findPageByTitle`). Three small recursive helpers, one shared traversal — that's the whole data layer.

## Recursive Includes

Tree's markup layer is two files. The root template renders the top-level list and hands each page to an include:

```html
<!-- com.realmacsoftware.navTree/templates/index.html -->
<!-- LEVEL 1 -->
<ul class="{{classes.list}}">
    @each(page in pages)
        @include("item", page: page)
    @endeach
</ul>
```

The include is where the technique lives. `include/item.html` renders one node — and for that node's children, includes **itself**. This is the full file (only the decorative chevron SVG is elided):

```html
<!-- com.realmacsoftware.navTree/templates/include/item.html -->
@if(page.hasPages)
<li role="none" class="group">
    <div
        id="{{page.id}}"
        tabindex="{{page.index}}"
        role="treeitem"
        :aria-expanded="isOpen('{{page.id}}')"
        @click="toggle('{{page.id}}')"
        @keydown.enter.prevent="toggle('{{page.id}}')"
        @keydown.space.prevent="toggle('{{page.id}}')"
        @focus="setCurrent('{{page.id}}')"
        class="{{classes.item}} @if(page.isTopLevel) {{classes.topLevel}} @elseif(page.isSecondLevel) {{classes.subMenuItem}} @elseif(page.isThirdLevel) {{classes.thirdLevelItem}} @endif"
        :aria-current="({{page.isActive}} || {{page.hasActiveChild}}) ? 'page' : null"
    >
        @if(page.showPageIcon)<div class="{{classes.pageIcon}}">{{page.icon}}</div>@endif
        <button type="button" class="{{classes.iconWrapper}}"
            :aria-label="isOpen('{{page.id}}') ? 'Collapse {{page.title}}' : 'Expand {{page.title}}'"
            aria-hidden="true"
            :class="{ 'rotate-90': isOpen('{{page.id}}') }"
        >
            @if(!hasSvgIcon)<svg><!-- … chevron path … --></svg>@else {{svgIcon}} @endif
        </button>
        @if(page.isFolder)
        <span class="{{classes.title}}"> {{page.title}} </span>
        @else
        <a href="{{page.url}}" class="{{classes.title}}" @if(page.openInNewWindow) target="_blank" @endif> {{page.title}}</a>
        @endif
    </div>

    @if(showSubMenus) @if(page.hasPages)
    <ul
        x-show="isOpen('{{page.id}}')"
        x-collapse.duration.{{collapseDuration}}
        role="group"
        class="@if(page.isTopLevel) {{classes.subMenu}} @elseif(page.isSecondLevel) {{classes.thirdLevel}} @elseif(page.isThirdLevel) {{classes.thirdLevel}} @endif"
    >
        @each(subPage in page.pages) @include("item", page: subPage) @endeach
    </ul>
    @endif @endif
</li>
@else
<!-- SINGLE LINK -->
<li role="none">
    <a
        href="{{page.url}}"
        id="{{page.id}}"
        tabindex="{{page.index}}"
        role="treeitem"
        @focus="setCurrent('{{page.id}}')"
        class="{{classes.item}} @if(page.isTopLevel) {{classes.topLevel}} @elseif(page.isSecondLevel) {{classes.subMenuItem}} @elseif(page.isThirdLevel) {{classes.thirdLevelItem}} @endif"
        :aria-current="({{page.isActive}} || {{page.hasActiveChild}}) ? 'page' : null"
        @if(page.openInNewWindow) target="_blank" @endif
    >
        @if(page.showPageIcon)<div class="{{classes.pageIcon}}">{{page.icon}}</div>@endif {{page.title}}
    </a>
</li>
@endif
```

Walk it top to bottom:

* **Line 1, `@if(page.hasPages)`** — the whole file is one fork: branch nodes (pages with children) take the first half, leaves take the `@else` half. This test is the recursion's brain.
* **The branch header `<div role="treeitem">`** — carries the hook-built `page.id` into every Alpine call: `isOpen('{{page.id}}')`, `toggle('{{page.id}}')`, `setCurrent('{{page.id}}')`. The template interpolates data; the Alpine component (registered once via `@portal(bodyEnd, includeOnce: true)` in `index.html`) owns all state, including keyboard navigation and the roving tabindex.
* **The level-class chain** — `@if(page.isTopLevel) … @elseif(page.isSecondLevel) … @elseif(page.isThirdLevel) …` picks styling per depth. The same include file renders every level; only the precomputed booleans change. Note that levels three-and-deeper share one style — unbounded *structure* doesn't require unbounded *styling*.
* **`:aria-current="({{page.isActive}} || {{page.hasActiveChild}}) ? 'page' : null"`** — template `@if` can't express `||`, but interpolating two booleans into a client-side Alpine expression can. The rendered output is plain JavaScript like `(true || false) ? 'page' : null`.
* **`@if(page.isFolder)`** — folders get a `<span>` (nothing to link to), real pages get an `<a href="{{page.url}}">`.
* **`@if(showSubMenus) @if(page.hasPages)`** — two nested single-condition `@if`s are the template-language spelling of AND. `showSubMenus` comes from the hook: always `true` when published, but on the canvas it's the user's **Preview Sub Menus** switch.
* **The recursive line** — `@each(subPage in page.pages) @include("item", page: subPage) @endeach`. Each child is passed back into the same file *under the same name*, `page:`. That renaming is what makes recursion work: `item.html` is written against a single contract — "I receive one page object called `page`" — and never knows or cares which level it's rendering.
* **The `@else` leaf branch** — a plain link with no `@include("item")` anywhere in it. This is the base case.

**Termination** needs no counter and no special directive. Recursion only re-enters through the branch half, which is guarded by `page.hasPages`; every child either has children (recurse again) or doesn't (render the leaf and stop). Because the hook already truncated the tree — `children` is `[]` past the depth limit, which makes `hasPages` false — the template's recursion depth is bounded by the data, and the data is bounded by the hook. If you write your own recursive include, preserve both properties: a guarded self-include and a leaf branch that includes nothing.

Two mechanical rules from the [@include reference](../component/language/include.md#recursive-includes) apply doubly here: the file must live in `templates/include/` (only that directory is resolvable by name), and a mistyped template name fails *silently* — in a recursive setup that means your entire tree below level one quietly vanishes, so check the include name first when a nav renders only its top level.

## One Tree, Two Menus: The Desktop/Mobile Split

Menu (`com.realmacsoftware.navbar`) answers a different question: what if one page tree needs two completely different renderings? Its `templates/include/` holds a dozen partials split by filename prefix — `desktop_item`, `desktop_folder`, `desktop_submenu`, `desktop_submenu_menu`, `desktop_submenu_indicator`, and `mobile_*` counterparts, plus `logo` and `title` (the prefix convention the [@include best practices](../component/language/include.md#best-practices) recommend). `index.html` walks the **same `pages` prop twice**, dispatching into each family:

```html
<!-- com.realmacsoftware.navbar/templates/index.html -->
<!-- Desktop items -->
<div class="{{classes.desktop.items}}">
    @each(page in pages) @include("desktop_item") @endeach
</div>
<!-- … -->
@if(includeMobileMenu) @portal("bodyStart")
<!-- … backdrop and slide-over chrome … -->
<nav>
    <ul class="{{classes.mobile.items}}">
        @each(page in pages) @if(page.isFolder)
        @include("mobile_folder") @else @include("mobile_item") @endif
        @endeach
    </ul>
</nav>
<!-- … -->
@endportal @endif
```

The desktop tree renders inline in the header as hover-driven dropdowns; the mobile tree renders through `@portal("bodyStart")` as a click-driven slide-over that can overlay the whole page. One hook, one filtered tree, two markup worlds — all the data work is shared, all the presentation is per-device. Note the contrast with Tree: Menu's includes chain *fixed* levels (`desktop_item` → `desktop_submenu` → `desktop_submenu_menu`, three deep) instead of self-including, because a dropdown menu has a sensible maximum depth where a sidebar tree doesn't. Pick the pattern that matches your markup: self-include for unbounded trees, a chain of level-specific includes when each level genuinely looks different.

## Active States and aria-current

Menu's hook computes ancestor-active state with a deliberate subtlety — it checks the **raw** tree, not the filtered one:

```javascript
// com.realmacsoftware.navbar/hooks.source.js
// Checks the raw page tree so an active page hidden from the menu
// (displayInMenu == false) still highlights its ancestor folders
const hasActiveDescendant = (page) =>
    (page.pages || []).some(
        (child) => child.isActive || hasActiveDescendant(child)
    );

// Recursive function to filter pages
const filterPages = (pages) => {
    return pages
        .filter((page) => page.displayInMenu && !page.isDraft)
        .map((page) => {
            const filteredPages = page.pages ? filterPages(page.pages) : null;
            return {
                ...page,
                pages: filteredPages,
                hasPages: filteredPages ? filteredPages.length > 0 : false,
                hasActiveChild: hasActiveDescendant(page),
            };
        });
};

// Apply the recursive filter to the top-level pages
const pages = filterPages(rw.pages);
```

If the current page is hidden from the menu, its parent folder should still light up — so `hasActiveChild` is derived from `page.pages` (the unfiltered children) even though the rendered list uses `filteredPages`. Tree computes the same flag from filtered children instead; both are defensible, but Menu's version is the one to copy when hidden-but-active pages are possible.

In the templates, the flags become attributes. Menu emits the accessibility standard `aria-current="page"` on the active link and a styling hook on ancestors:

```html
<!-- com.realmacsoftware.navbar/templates/include/desktop_item.html -->
<a
    @if(page.openInNewWindow) target="_blank" @endif
    href="{{page.url}}"
    @mouseover="handleMouseEnter"
    @mouseleave="handleMouseLeave"
    class="flex items-center {{classes.desktop.item}}"
    @if(page.isActive)
    aria-current="page"
    @endif
    @if(page.hasActiveChild)
    data-active-child
    @endif
>
    {{page.title}} @includeIf(page.hasPages, template:
    "desktop_submenu_indicator")
</a>
```

Every partial in both families repeats this pair, so the active trail is visible (and stylable via `[aria-current="page"]` and `[data-active-child]` selectors) at every depth. Tree renders the same information dynamically instead — the `:aria-current` Alpine binding you saw in `item.html` marks a node when it's active *or* on the active trail. Whichever variant you choose, emit `aria-current="page"` on exactly one link per menu; screen readers announce it, and it doubles as your styling hook, replacing invented `active` classes.

## The Nav on the Canvas

Navigation components hit two edit-mode snags. First, canvas chrome: Elements injects drop areas into the editing canvas, and Menu ships a three-line `templates/editor.css` just to keep them from distorting the navbar layout:

```css
[data-rwx-droparea] {
    width: auto !important;
}
```

How editor-only stylesheets work — and why wrapping them in `@if(edit)` is the better habit — is covered in [Designing the Edit-Mode Experience](edit-mode-experience.md#editor-only-css). Second, sparse projects: users often build navs in a project that has one page so far, which makes the filtered tree a single lonely item and submenus impossible to see. The core components answer with preview switches rather than fake data — Tree's **Preview Sub Menus** switch (`showSubMenus` is forced on when published, user-controlled on the canvas) and Menu's mobile-menu preview switch. If your nav renders literally nothing in a one-page project, fall back to the [empty-state placeholder pattern](edit-mode-experience.md#empty-state-placeholders) so users still see something stylable.

## The deploy Flag

Tree's `info.json` is also the core pack's only component to set the `deploy` key explicitly:

```json
{
    "identifier": "com.realmacsoftware.navTree",
    "title": "Tree",
    "group": "Navigation",
    "helpURL": "../../elements/components/tree.md",
    "deploy": true
}
```

Per the [info.json reference](../component/info.json.md), `deploy` controls whether the component is included when deploying a pack, and it defaults to `true` — so Tree's entry just states the default out loud. The flag earns its keep set to `false`: internal helper components, test harnesses, or half-finished experiments living in your dev pack can be excluded from the deployed pack without deleting them. If you keep private scaffolding alongside shippable components, mark it `"deploy": false`.

## Related Documentation

* [rw.pages](../component/hooks.js/available-data/rw.pages.md) — the full page-object field reference
* [@include](../component/language/include.md) — include resolution, parameters, and recursion
* [@each](../component/language/each.md) — iterating arrays in templates
* [Designing the Edit-Mode Experience](edit-mode-experience.md) — editor CSS, placeholders, and preview switches
* [info.json](../component/info.json.md) — the `deploy` flag and other component metadata
