---
description: Design families of components that work together
---

# Component Suites & Cross-Component Communication

Some problems are too big for one component. A modal needs a close button the user can style and place freely. A filterable grid needs a search input *and* a row of tag buttons, and neither belongs inside the grid's markup. The answer is a **suite**: several small components that ship together, find each other at runtime, and cooperate. This guide covers when to split a component into a suite, the three communication channels the Core Pack uses to connect suite members — window events, a shared Alpine store, and page-level engines wired through shared templates — plus the quieter fourth option: children that discover their parent through the DOM.

{% hint style="success" %}
This guide dissects the **Filter** (`com.realmacsoftware.filter`), **Filter Tags** (`com.realmacsoftware.filterTags`), **Modal** / **Modal Close** (`com.realmacsoftware.modal`, `com.realmacsoftware.modalClose`), and **Reveal** (`com.realmacsoftware.reveal`) components from the open-source [Core Pack](../development-resources/open-source-components.md). Open their source alongside this page.
{% endhint %}

## When One Component Should Become Several

Split when you notice any of these:

* **Inspector overload.** You keep adding properties to configure a sub-part — "Show close button", "Close button position", "Close button icon", "Close button color". Every switch is a decision you made for the user. The Core Pack's answer is Modal Close: instead of a stack of inspector controls, the close button is a *component* the user drops in, styles like anything else, and places anywhere inside the modal.
* **Reusable, repeatable children.** A form has an unpredictable number of fields; a filter UI might need the search input in a sidebar and the tag buttons above the grid. When you can't predict how many children there are or where they go, each child should be its own component.
* **A dropzone isn't enough.** [`@dropzone`](../component/language/dropzone.md) gives users a hole to fill, but the filling is inert — it has no inspector of its own, no hooks, no behaviour. The moment the thing *inside* the hole needs logic — a button that knows how to close its modal, a field that validates itself — promote it to a component.

Stay single when the repeating parts are pure markup driven by data: tabs, table rows, and slides are better served by a collection and an `@each` loop — see [Collection-Driven Dropzones](./collection-driven-dropzones.md).

Once you split, the parts need a way to talk. There are three channels, plus DOM ancestry:

| Channel | Coupling | Core example | Reach for it when |
| --- | --- | --- | --- |
| Window events | An agreed event name and payload | Modal trigger → Modal panel | One-shot signals: open, close, notify |
| Alpine store | A shared singleton, keyed by group id | Filter + Filter Tags | Several components read/write ongoing state |
| Shared page engine | `data-*` attributes read by one script | Reveal + its GSAP engine | Many instances, one behaviour, zero per-instance JS |
| DOM ancestry | Child must render inside parent | Modal Close, form fields | The relationship *is* containment |

## Channel 1: Window Events

The lightest channel. Sender and receiver share nothing but an event name and a payload shape — they don't reference each other, don't share state, and can be authored in different packs. The Modal pair is the canonical example. The trigger dispatches an event that bubbles to `window`:

```html
<!-- templates/index.html (Modal) — the sender -->
<span
    @click="$dispatch('open-modal', { id: '{{id}}' })"
    class="{{classes.trigger}}"
>
    @dropzone("trigger", title: "Trigger")
</span>
```

And the teleported panel — no longer a DOM descendant of the trigger once `@portal` has moved it — listens at the window level and compares the payload against its own instance id:

```html
<!-- templates/index.html (Modal) — the receiver, inside the @portal("bodyEnd") block -->
@open-modal.window="(e) => { open = e.detail.id === '{{id}}' }"
```

Every panel on the page hears every `open-modal` event; the id comparison means only the matching panel opens — and, because the comparison result is *assigned* rather than used as a guard, every other modal sets `open = false` at the same time. One convention, two attributes, and the suite coordinates itself.

That is deliberately all this guide says about events, because [Modals, Overlays & Portals](./modals-overlays-and-portals.md) walks the whole pattern in depth — the portal split, the id handshake, and the edit-mode handling. The same shape powers the Accordion's group behaviour, dissected in [Interactive Components with Alpine.js](./interactive-components-with-alpine.md). Use events when the message is a *moment* ("open now"). When components need to share *state that persists* — a query string, a set of active tags — you want the next channel.

## Channel 2: A Shared Alpine Store

Filter and Filter Tags are two inspector-light components that drive the same outcome: showing and hiding items in a grid. They never reference each other. Instead, both talk to a page-level singleton — an Alpine store named `filters` — and the items being filtered are ordinary layout components that advertise themselves with `data-*` attributes. Three parties, one shared blackboard.

### The Store: One Singleton, Many Groups

The store lives in the Core Pack's shared assets and is loaded once per page by a shared template (`shared/templates/headEnd/alpine-directives.html` — the same mechanism as Channel 3). Everything inside it is keyed by a `listId`, which is what lets any number of independent filter groups coexist on one page:

```javascript
// shared/assets/alpine-store-filters.js (trimmed)
document.addEventListener('alpine:init', () => {
    Alpine.store('filters', {
        lists: {},
        filteredLists: {},
        observers: {},  // Store observers by listId

        registerList(listId, options = {}) {
            // … guard against a missing listId …
            if (this.lists[listId]) {
                this.mergeOptions(this.lists[listId].options, options);
                return;
            }

            this.lists[listId] = this.createList();
            this.mergeOptions(this.lists[listId].options, options);

            this.addItemsToList(listId);

            this.observers[listId] = new MutationObserver(/* … re-index items that arrive later … */);
            this.observers[listId].observe(document.body, { childList: true, subtree: true });
        },

        addItemsToList(listId) {
            const elements = document.querySelectorAll(`[data-filter-group="${listId}"]`);
            this.filteredLists[listId] = Array.from(elements).map(element =>
                this.createItem(element)
            );
            this.filterList(listId);
            this.setTags(listId);
        },

        // … updateQuery, toggleTag, isActiveTag, getTags, filterList, matches, transition …
    });
});
```

Two design decisions here carry the whole suite. First, `registerList` is **idempotent**: if the list already exists, it merges the new options and returns. That means Filter and Filter Tags can both register the same group in *any order* — whichever initialises first creates the list, the second just contributes its options. Suite members never need to know who arrived first. Second, the store finds its items by **querying the DOM** for `[data-filter-group="listId"]` — so anything that renders that attribute is filterable, with a `MutationObserver` catching items added after load.

### Writing: The Filter Input

The Filter component is a search input whose entire job is writing one value into the store. Its template registers a tiny factory (note that a portal's `includeOnce` id only has to be unique — the Filter's carries a legacy name) and binds the input:

```html
<!-- templates/index.html (Filter) -->
@portal(bodyEnd, id: "com.realmacsoftware.accordionFilter.alpine", includeOnce: true)
<script>
    document.addEventListener('alpine:init', function() {
      Alpine.data('filter', (groupId) => ({
        groupId,
        q: '',
        init() {
          Alpine.store('filters').registerList(this.groupId);
          this.$watch('q', (value) => {
            Alpine.store('filters').updateQuery(this.groupId, value);
          });
        }
      }));
  });
</script>
@endportal

<input 
    type="search"
    x-model="q"
    placeholder="{{placeholder}}"
    class="{{classes.input}}"
    aria-label="{{placeholder}}"
>
```

`x-model` binds the input to local state `q`; the `$watch` forwards every keystroke into the store via `updateQuery`, which re-runs the group's `filterList`. The instance is wired to its group in `hooks.js`:

```javascript
// hooks.source.js (Filter)
const filter = globalFilter(rw);

rw.setRootElement({
    as: "div",
    class: classes.wrapper,
    args: {
        "x-data": `filter('${filter.filterGroupId}')`,
        ...filter.args,
    },
});
```

### Reading: Filter Tags

Filter Tags never sees the search input. It renders one button per tag the store discovered, and every interaction is a store call:

```html
<!-- templates/index.html (Filter Tags) -->
@portal(bodyEnd, id: "com.realmacsoftware.filterTags.alpine", includeOnce: true)
<script>
  document.addEventListener('alpine:init', function() {
    Alpine.data('filterTags', (groupId, options) => ({
      groupId,
      options,
      init() {
        Alpine.store('filters').registerList(this.groupId, { tags: this.options });
      },
      toggle(tag) {
        Alpine.store('filters').toggleTag(this.groupId, tag);
      },
      isActive(tag) {
        return Alpine.store('filters').isActiveTag(this.groupId, tag);
      },
      get tags() {
        return Alpine.store('filters').getTags(this.groupId);
      }
    }));
  });
</script>
@endportal

@if(edit)
  <button class="{{classes.tag}}">Example Tag</button>
  <button class="{{classes.tag}}" data-active="true">Active Tag</button>
@endif
<template x-for="tag in tags" :key="tag">
    <button 
        @click="toggle(tag)"
        :data-active="isActive(tag)"
        x-text="tag"
        class="{{classes.tag}}"
    ></button>
</template>
```

The `get tags()` getter makes the button list *reactive*: because it reads from the store, Alpine re-renders the `x-for` whenever the store's tag set changes — including when the `MutationObserver` indexes items that arrived after load. The `@if(edit)` block is a nice suite touch: on the canvas, where no real items exist yet, the user still sees placeholder tags instead of an empty gap (see [Designing the Edit-Mode Experience](./edit-mode-experience.md)). Note also `:data-active="isActive(tag)"` — active styling is driven by `data-[active=true]:` Tailwind variants computed in `hooks.js`, so the store never touches classes.

### Namespacing: How Groups Get Their Ids

Both components resolve their group id through the shared `globalFilter` build helper (documented under [Build Tools](../development-resources/build-tools/shared-hooks/interactive/global-filter.md)). Reformatted from the compiled hooks bundle:

```javascript
// shared build helper globalFilter (compiled bundle, reformatted)
globalFilter = (rw) => {
    const {
        globalFilterEnable: wantsFilter,
        globalFilterGroup: group,
        globalFilterCustomGroupId: groupId,
        globalFilterTransition: transition = null,
    } = rw.props;
    const { parent } = rw.node;
    const filterGroupId = group == "parent" ? parent.id : groupId;
    return {
        wantsFilter,
        filterGroupId,
        transition,
        args: wantsFilter
            ? { "data-filter-group": filterGroupId, "data-filter-transition": transition }
            : {},
    };
};
```

The line that matters is `group == "parent" ? parent.id : groupId`. By default the group id is **the parent component's instance id** ([`rw.node.parent.id`](../component/hooks.js/available-data/rw.node.md)) — so a Filter, a Filter Tags, and a grid of items dropped into the *same container* automatically share a group with zero configuration, and a second container elsewhere on the page forms a second, fully independent group. When the controls can't live beside their items, the inspector's **Group → Custom** option substitutes a user-typed id, letting a search field in a sidebar drive a grid in the main column.

The third party — the items — emits the same attributes from the other side. Layout components like Container run the same helper and spread its `args`, plus the user's tags from a collection:

```javascript
// hooks.source.js (Container, excerpts)
const { tags, attributes } = rw.collections;
const dataTags = tags?.map((tag) => tag.title).join(",") || "";
// …
const filter = globalFilter(rw);
// …
rw.setRootElement({
    as: link.hasLink ? "a" : globalHTMLTag(rw, "div"),
    class: classes.wrapper,
    args: {
        id: globalID,
        ...link.args,
        ...filter.args,
        "data-filter-tags": dataTags,
        ...customAttributes,
    },
});
```

### The Flow End to End

1. The user drops Containers into a grid and enables **Filter** on each, tagging them via a collection. Each renders `data-filter-group="<parentId>" data-filter-tags="design,2024"`.
2. A Filter and a Filter Tags dropped into the same parent resolve the same `<parentId>` at build time — no runtime discovery needed.
3. On `alpine:init`, whichever control initialises first calls `registerList('<parentId>')`; the store queries `[data-filter-group="<parentId>"]`, indexes each item's text and tags, and starts observing for late arrivals. The second control's `registerList` merges its options into the existing list.
4. Typing calls `updateQuery`; clicking a tag calls `toggleTag`. Both funnel into `filterList`, which runs every item through `matches` (text *and* tags must match) and transitions visibility.
5. Filter Tags' reactive `tags` getter keeps the button row in sync with whatever the store has indexed.

The store pattern beats events whenever state outlives the moment: a new suite member (a "clear filters" button, a results counter) just reads the same store keyed by the same group id — no changes to Filter, Filter Tags, or the items.

## Channel 3: Page-Level Engines via Shared Templates

The third channel removes per-instance JavaScript entirely. Reveal — the Core Pack's scroll-animation component — ships **no script of its own**. Its template is a single line (`@dropzone("content", title: "Content")`); its `hooks.js` compiles the inspector settings into `data-*` attributes on the root element:

```javascript
// hooks.source.js (Reveal)
const transformHook = (rw) => {
  const { id } = rw.node;
  const reveal = globalReveal(rw);
  // … classes elided …
  rw.setRootElement({
    as: globalHTMLTag(rw, "div"),
    class: classes,
    args: { ...reveal }
  });
  // …
};
```

The shared [`globalReveal`](../development-resources/build-tools/shared-hooks/animations/global-reveal.md) helper returns nothing but attributes (reformatted from the compiled bundle):

```javascript
// shared build helper globalReveal — the returned attributes (compiled bundle, reformatted)
globalReveal = (rw) => {
    // … read the reveal props, build animation names and GSAP trigger points …
    return {
        "data-reveal": "",
        "data-reveal-id": revealID,
        "data-reveal-duration": `${duration / 1e3}`,
        "data-reveal-animation": animationName,
        "data-reveal-exit-animation": exitAnimationName,
        "data-reveal-play": play,
        "data-reveal-start": gsapTriggerPoints[start] || gsapTriggerPoints["entering-screen"],
        "data-reveal-end": gsapTriggerPoints[end] || gsapTriggerPoints["exiting-screen"],
        // … delay, easing, distance, degrees, scrub, debug …
    };
};
```

The behaviour lives in one **engine**, registered page-wide through the pack's [shared templates](../component/shared-files/templates.md) — GSAP and ScrollTrigger load from `shared/templates/headStart/setup.html`, and the engine itself is injected at `bodyEnd`, where it sweeps the page for anything carrying the contract attribute:

```html
<!-- shared/templates/bodyEnd/reveal.html (trimmed) -->
<script>
    gsap.registerPlugin(ScrollTrigger);
    document.addEventListener("DOMContentLoaded", () => {
        const revealElements = document.querySelectorAll("[data-reveal]");
        revealElements.forEach((element, index) => {
            // … hide the element until its animation runs …
            const {
                revealAnimation: animation = "fadeUpIn",
                revealExitAnimation: exitAnimation = "fadeUpOut",
                revealPlay: play = "enter-exit",
                revealStart: start = "top bottom",
                revealEnd: end = "top top",
                // … delay, duration, easing, distance, degrees, scrub, debug …
                revealId,
            } = element.dataset;

            // … parse numbers and flags, build the shared config and a unique trigger id …
            ScrollTrigger.create({
                trigger: element,
                start: start,
                end: end,
                id,
                onEnter: () => {
                    if (playOnce && triggeredOnce) return;
                    element.style.transitionProperty = "none";
                    triggeredOnce = true;
                    gsap.effects[animation](element, config);
                },
                // … onLeave / onEnterBack / onLeaveBack mirror this with the exit animation …
            });
        });
    });
</script>
```

Note the defaults in the destructuring: every attribute is optional, so the engine tolerates emitters that only set what they care about. That's what makes this a *channel* rather than a private implementation detail — the contract is "carry `data-reveal` plus any overrides", and it doesn't matter which component (or which pack helper) emitted the attributes.

### Shared Template or includeOnce Portal?

Both give you exactly one copy of a script per page, so choose by scope:

* **`@portal(bodyEnd, includeOnce: true, id: …)`** belongs to one component and ships **only when that component is used**. It's the right home for a factory that only its own component instantiates — the Accordion, Tabs, and Filter factories all live this way.
* **Shared templates** are emitted once per page whenever *any* component from your pack is present ([Shared Files](../component/shared-files/README.md)). Choose them when the code is genuinely pack-level: several components depend on it (the Alpine runtime, the `filters` store), the contract is attribute-based so *any* emitter can participate (the Reveal engine), or the pieces must land at different injection points in the right order (libraries in `headStart`, engine in `bodyEnd` — a single portal can't span locations).

The trade-off is bytes: a shared template rides along on every page that uses your pack, even pages where no instance needs it. Keep engines lean, and keep per-component factories in portals.

## Parent/Child Contracts Without Events

Sometimes the relationship between suite members *is* containment — a field only means something inside its form. In that case you don't need events or stores at all: the parent marks its rendered root, and children find it at runtime with DOM traversal. You've already seen the Core Pack version — Modal Close calls `$dialog.close()`, which resolves the nearest enclosing dialog by ancestry. Here is the generic skeleton, as a form suite:

```html
<!-- com.example.form — templates/index.html -->
<form data-form-id="{{id}}" action="{{action}}" method="post" class="flex flex-col gap-4">
    @dropzone("fields", title: "Fields")
</form>
```

The parent's whole contribution to the contract is one attribute: `data-form-id`, carrying its instance id (`id` and `action` are forwarded by a tiny `hooks.js` — `rw.setProps({ id: rw.node.id, action })` — exactly like every other example in these guides). Child fields render ordinary inputs, with `label` and `fieldName` as plain text properties:

```html
<!-- com.example.formField — templates/index.html -->
@include("alpine")

<label class="flex flex-col gap-1">
    <span class="text-sm font-medium">{{label}}</span>
    <input type="text" name="{{fieldName}}" x-data="exampleFormField()" class="rounded border px-3 py-2">
</label>
```

And the factory discovers the parent the moment it initialises:

```html
<!-- com.example.formField — templates/alpine.html -->
@portal(bodyEnd, includeOnce: true, id: "com.example.formField.alpine")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("exampleFormField", () => ({
            form: null,
            init() {
                // Discover the parent at runtime: the nearest ancestor rendered by com.example.form
                this.form = this.$el.closest("form[data-form-id]");
                if (!this.form) return;
                this.form.addEventListener("submit", (e) => {
                    if (!this.$el.checkValidity()) e.preventDefault();
                });
            },
        }));
    });
</script>
@endportal
```

`closest()` makes the child position-independent: the user can nest the field inside grids, flex wrappers, or anything else dropped into the `fields` dropzone, and it still finds its form. The contract stays one attribute deep, so the parent can evolve freely. The full architecture — field types, validation, submission handling — is covered in [Building Form Components](./building-form-components.md), coming in this section.

## Packaging a Suite

A suite is also a product-design exercise: the pieces must be discoverable together and hard to misuse.

* **Group suite members in the palette.** The `group` key in each component's [`info.json`](../component/info.json.md) must be one of the pre-defined categories, and components with the same category are grouped together in the UI — which is why Modal, Modal Close, Filter, and Filter Tags all ship as `"group": "Interactive"` and sit side by side. You can't invent a category per suite, so use the `tags` array to make members co-searchable (both filter components should surface for "filter").
* **`requiresPhp` is effectively inherited.** Per the [`info.json` reference](../component/info.json.md), the flag is "not needed for child Components that only ever appear nested inside another Component that already requires PHP". If `com.example.form` gains server-side handling and sets `requiresPhp: true`, field components that only ever render inside it can omit the flag.
* **Keep child inspectors minimal.** A child that needs its parent for meaning should hold only the properties that describe *itself* — a field's label and name, a close button's cursor. Anything about the relationship (grouping, ids, wiring) belongs to the parent or is derived automatically, the way `globalFilter` derives the group from `rw.node.parent.id`. Modal Close's inspector is a fraction of Modal's; that asymmetry is a sign the split is right.
* **Warn when a child is orphaned.** A Form Field dropped outside any Form silently does nothing — tell the user on the canvas instead. You might expect to compute `isOrphaned` in `hooks.js`, but [`rw.node.parent`](../component/hooks.js/available-data/rw.node.md) exposes only the parent instance's `id` and its `container` name — not *which component* the parent is — so hooks can't distinguish your Form from any other component with a dropzone. The rendered DOM, however, carries the real contract, and Alpine runs on the edit canvas, so do the check in the browser and gate the banner with `@if(edit)`:

```html
<!-- com.example.formField — templates/index.html (excerpt) -->
@if(edit)
<div
    x-data="{ isOrphaned: false }"
    x-init="isOrphaned = !$el.closest('form[data-form-id]')"
    x-show="isOrphaned"
    class="rounded border border-amber-400 bg-amber-100 px-3 py-2 text-sm text-amber-900"
>
    Form Field works inside a Form component — drag it into a Form's Fields area to wire it up.
</div>
@endif
```

The banner ships zero bytes to published pages — the whole block is compiled away outside edit mode. If your child can *partially* work standalone, prefer a quieter hint over a warning; reserve loud banners for children that genuinely do nothing alone.

## Related Documentation

* [Modals, Overlays & Portals](./modals-overlays-and-portals.md) — the window-event handshake in full depth
* [Interactive Components with Alpine.js](./interactive-components-with-alpine.md) — factories, `alpine:init`, and instance wiring
* [Shared Files](../component/shared-files/README.md) — pack-level assets and templates
* [Shared Templates](../component/shared-files/templates.md) — injection points and once-per-page behaviour
* [`rw.node`](../component/hooks.js/available-data/rw.node.md) — what hooks can (and can't) know about a component's parent
* [Building Form Components](./building-form-components.md) — the form suite architecture, end to end
