---
description: Structure stateful, interactive components using Alpine.js factories
---

# Interactive Components with Alpine.js

Every interactive component faces the same structural problem: the behaviour is shared, but the state is not. Ten accordions on a page need one copy of the toggle logic and ten independent `open` flags. This guide shows the pattern the core components use to solve it — an Alpine.js **factory** registered once per page through a portal, instantiated per component instance from `x-data` — and everything that hangs off that pattern: wiring instances from `hooks.js`, passing configuration safely, grouping bindings, shipping styles, animation lifecycles, and accessibility.

{% hint style="success" %}
This guide dissects the **Accordion** (`com.realmacsoftware.accordion`), **Tabs** (`com.realmacsoftware.tabs`), and **Content Slider** (`com.realmacsoftware.contentSlider`) components from the open-source [Core Pack](../development-resources/open-source-components.md). Open their source alongside this page.
{% endhint %}

## Why Alpine.js

Alpine is already on the page. The Core Pack loads Alpine v3 and a set of official plugins on every page through a shared `headStart` template, so the core components — and any component built alongside them — can assume the runtime exists:

```html
<!-- shared/templates/headStart/setup.html -->
<script defer src="{{assetPath}}/alpine-collapse.js"></script>
<script defer src="{{assetPath}}/alpine-focus.js"></script>
<script defer src="{{assetPath}}/alpine-intersect.js"></script>
<script defer src="{{assetPath}}/alpine-ui.js"></script>
<script defer src="{{assetPath}}/alpine.js"></script>
<!-- … smooth-scroll and GSAP scripts … -->
```

The plugin files live in the Core Pack's `shared/assets/` folder and each one unlocks directives you'll see throughout the core components:

* `alpine.js` — the Alpine v3 core (`x-data`, `x-bind`, `x-show`, `$watch`, `$dispatch`, …)
* `alpine-collapse.js` — `x-collapse`, used by the Accordion's content panel
* `alpine-focus.js` — focus trapping for overlays
* `alpine-intersect.js` — `x-intersect`, for triggering behaviour on scroll into view
* `alpine-ui.js` — UI primitives such as `x-dialog`, used by the Modal component

Note the load order: the plugins are listed *before* `alpine.js`. Each plugin registers itself on the `alpine:init` event, so as long as everything loads before Alpine starts, registration order takes care of itself. Your component scripts hook into the exact same event.

Beyond availability, Alpine fits Elements well because it is declarative. State lives on an element (`x-data`), behaviour is expressed as attributes (`x-bind`, `x-show`, `@click`), and the Elements template engine is already in the business of generating attributes. There is no build step, no virtual DOM, and no mounting code to keep in sync with your markup.

## The Factory Pattern

The naive approach to component JavaScript — a `<script>` block in `index.html` — is emitted once **per instance**. Ten accordions means ten copies of the same logic. The core components invert this: the logic is registered exactly once as a named factory, and each instance calls the factory with its own ID and options.

The Accordion is the canonical example, and it also shows what makes the pattern more than deduplication: instances of the same factory can **coordinate through events** without any shared registry. When one accordion opens, it broadcasts; every accordion in the same group hears the broadcast and closes itself:

```html
<!-- templates/alpine.html (Accordion) -->
@portal(bodyEnd, includeOnce: true, id: "com.realmacsoftware.accordion.alpine")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("accordion", (id, options = {}) => ({
            open: options.openOnLoad || false,
            id,
            options,
            init() {
                this.$watch("open", (value) => {
                    if (value && this.options.groupId) {
                        this.$dispatch("close-accordions-in-group", {
                            groupId: this.options.groupId,
                            id: this.id,
                        });
                    }
                });
            },

            details: {
                ["@close-accordions-in-group.window"](e) {
                    const { groupId, id } = e.detail;
                    if (groupId == this.options.groupId && id != this.id) {
                        this.open = false;
                    }
                },
                // … :data-open binding elided …
            },
            // … summary and content binding groups elided …
        }));
    });
</script>
@endportal
```

Three details of the wrapper are load-bearing for any factory you write:

1. **`@portal(bodyEnd, …)`** moves the script to the end of `<body>`, regardless of where the component sits in the page.
2. **`includeOnce: true` with a reverse-DNS `id`** deduplicates the registration — one copy of the script no matter how many instances exist.
3. **`alpine:init`** registers the factory before Alpine parses the page's `x-data` attributes. Skipping the listener can *appear* to work in the edit canvas but fails in a published browser — see [JavaScript Templates](../component/templates/js-templates.md#alpinejs-integration) for why.

Now walk through the round trip. `init()` runs once per instance and uses `$watch` to observe that instance's own `open` flag. When `open` flips to `true` and the instance belongs to a group, `$dispatch` fires a `close-accordions-in-group` custom event, which bubbles up to `window`. Every accordion instance listens for it at the window level (`@close-accordions-in-group.window`), compares the payload against its own `groupId` and `id`, and closes itself if it's a sibling — but not the sender. No instance holds a reference to any other; the group membership is just data, computed in `hooks.js` from the components' shared parent.

This event-driven shape scales to whole component families — filters notifying reveal components, modal close buttons finding their modal — and is covered in depth in the component suites guide.

## Wiring Instances from hooks.js

The factory exists once; something has to call it per instance. The cleanest place to attach `x-data` is the component's root element, and the root element is built in `hooks.js` with [`rw.setRootElement()`](../component/hooks.js/available-functions/rw.setrootelement.md). Tabs shows the minimal version — the factory name plus two scalar arguments interpolated into the expression:

```javascript
// hooks.source.js (Tabs)
rw.setRootElement({
    as: "div",
    class: classes.wrapper,
    args: {
        "x-data": `elementsTabs('${id}', ${activeTabIndex})`,
        id: globalID || id,
    },
});
```

The `args` object becomes HTML attributes on the root element, so this renders as `<div x-data="elementsTabs('abc123', 0)" …>`. Because the expression is assembled in build-time JavaScript, you get full JS string handling — no wrestling with template syntax inside attribute values.

The Accordion's wiring is richer: it passes an options *object*, points `x-bind` at one of the factory's binding groups, and seeds the attributes Alpine will later control:

```javascript
// hooks.source.js (Accordion)
rw.setRootElement({
    as: "div",
    class: classes.details,
    args: {
        "x-data": `() => accordion('${id}', ${JSON.stringify({
            groupId: wantsGrouping ? groupId : null,
            openOnLoad: openOnLoad == "true",
        }).replace(/"/g, "'")})`,
        "x-bind": "details",
        "data-open": "false",
        role: "group",
        "aria-roledescription": "accordion",
        // … aria-label, id, and filter args elided …
    },
});
```

Two things to notice. The `JSON.stringify(…).replace(/"/g, "'")` dance swaps the JSON's double-quotes for single-quotes so the object literal survives inside a double-quoted HTML attribute — the *quote-swap* pattern, with trade-offs discussed in the next section. And `"data-open": "false"` is written out as a static attribute so the very first paint is correct *before* Alpine boots; once running, the factory's `:data-open` binding takes ownership of it.

Attaching `x-data` in `hooks.js` isn't mandatory. The Content Slider attaches it in template markup instead, which makes it easy to gate behaviour out of the edit canvas entirely:

```html
<!-- templates/index.html (Content Slider) -->
<div
    class="{{classes.swiper}}"
    @if(!edit)
    x-data="elementsContentSlider('{{id}}', {{swiperOptions}})"
    @endif
>
```

In edit mode the slider renders as plain markup — no Swiper instance fighting the canvas — while the published page gets the full behaviour. Use whichever home keeps the logic closest to what it depends on: `hooks.js` when the expression needs computed values, the template when it needs `@if(!edit)` gating around it.

## Passing Configuration Safely

Sooner or later your factory needs structured configuration — and interpolating raw JSON into `x-data="factory('{{id}}', {{configJson}})"` breaks, because the JSON's double-quotes terminate the HTML attribute. There are two working patterns: the quote-swap you saw in the Accordion's hook above, and a single-quoted `data-*` attribute that the factory reads back with `JSON.parse` in `init()`. The mechanics, the failure modes, and worked examples of both live in [JavaScript Templates](../component/templates/js-templates.md#alpinejs-integration) — this guide won't repeat them.

{% hint style="info" %}
**Recommended default:** embed configuration as a single-quoted `data-*` attribute (`data-config='{{configJson}}'`) and `JSON.parse` it in the factory's `init()`. It survives any double-quoted content in the data. Reserve the quote-swap for small config objects whose values you fully control, since it corrupts data containing quote characters. The ticker example later in this guide uses the `data-*` pattern end to end.
{% endhint %}

## Organizing State with Binding Groups

Look back at the Accordion factory and you'll see its behaviour isn't a flat bag of methods — it's organised into named objects (`details`, `summary`, `content`), one per element role in the markup. These are **binding groups**: objects whose keys are Alpine directives, applied wholesale to an element with `x-bind="groupName"`. Here are the two remaining groups from the Accordion factory:

```javascript
// templates/alpine.html (Accordion)
summary: {
    ["@click"]() {
        this.open = !this.open;
    },
},

content: {
    ["x-show"]() {
        return this.open;
    },
},
```

And here is the markup that consumes them. Each element opts into its role with a single `x-bind`, keeping the template free of inline handlers:

```html
<!-- templates/index.html (Accordion) -->
<div 
    x-bind="summary" 
    :id="'accordion-header-' + '{{id}}'"
    role="button"
    :aria-expanded="open.toString()" 
    :aria-controls="'accordion-content-' + '{{id}}'"
    class="{{classes.summary}}"
>
    <span class="flex-1 text-left">
        @dropzone("title", title: "Title")
    </span>
    <!-- … icon elided … -->
</div>
@if(showContent)
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
@endif
```

The division of labour is deliberate. *Behaviour* (the click handler, the show/hide rule) lives in the factory where it's written once and testable in one place. *Identity and structure* (IDs, ARIA relationships, classes) stay in the template where the template engine can interpolate per-instance values. When you change how toggling works, you edit one file; the markup never moves.

Note the `@if(!edit)` around `style="display: none;"` on the content panel. On a published page, Alpine takes a moment to boot; without that inline style, every closed accordion would flash its content before `x-show` kicks in. In the edit canvas the panel must stay visible so users can edit into the dropzone. One conditional attribute keeps both worlds correct — this is the recurring trick for sane edit/publish behaviour: **render the resting state statically, let Alpine take over after boot, and gate anything canvas-hostile behind `@if(!edit)`**. Tabs does the same with `x-cloak` on its panels, and pre-computes a `hideInEditor` flag per tab in `hooks.js` so the canvas shows exactly one panel without any JavaScript.

## Shipping Styles Through Portals

An `alpine.html` template isn't limited to one portal or to scripts. The Content Slider's template opens with a second portal that sends a stylesheet link and a `<style>` block to `headEnd` — again deduplicated with `includeOnce`, because these overrides are identical for every slider on the page:

```html
<!-- templates/alpine.html (Content Slider) -->
@portal(headEnd, id: "com.realmacsoftware.contentSlider.styles", includeOnce: true)
<link rel="stylesheet" href="{{componentAssetPath}}/swiper-bundle.min.css">
<style>
    .swiper-wrapper {
        margin: 0;
        padding: 0;
        list-style: none;
    }

    /* … slide and pagination rules elided … */

    /* Hide Swiper's default navigation button icons since we use custom SVGs */
    .swiper-button-prev::after,
    .swiper-button-next::after {
        display: none;
    }
    /* … further overrides elided … */
</style>
@endportal
```

Because the whole file runs through the template engine, `{{componentAssetPath}}` resolves to the component's own `assets/` folder at build time — and you can interpolate properties into the CSS the same way. The file's second portal (`bodyEnd`, `id: "com.realmacsoftware.contentSlider.script"`) loads `swiper-bundle.min.js` and registers the `elementsContentSlider` factory, so one template file fully describes the component's page-level footprint: styles in the head, behaviour at the end of the body, markup wherever the instance sits.

{% hint style="warning" %}
An `includeOnce` portal is emitted for the **first** instance only, so never interpolate per-instance property values inside one — every other instance's values would be silently dropped. Shared, identical content belongs in `includeOnce` portals; per-instance values belong on the instance's own markup (classes, `data-*` attributes, or a non-`includeOnce` portal).
{% endhint %}

## A Self-Contained Animation Component

Factories really pay off for components that *own a lifecycle* — anything with timers or animation loops that must start, pause, and clean up after themselves. Alpine calls `init()` when an instance's element appears and `destroy()` when it is removed, which gives you exact hooks for both ends. Here is a complete auto-scrolling ticker (`com.example.ticker`) demonstrating the full checklist: a `requestAnimationFrame` loop, pause on hover, respect for `prefers-reduced-motion`, a clean restart when the page returns from the back/forward cache, and symmetrical teardown.

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { speed, pauseOnHover } = rw.props;
    const { id } = rw.node;

    rw.setProps({
        id,
        edit: rw.project.mode === "edit",
        tickerJson: JSON.stringify({
            speed: Number(speed) || 60,
            pauseOnHover: pauseOnHover === true || pauseOnHover === "true",
        }),
    });
};
```

```html
<!-- templates/index.html -->
@include("alpine")

<div
    @if(!edit)
    x-data="exampleTicker('{{id}}')"
    x-bind="viewport"
    data-ticker-config='{{tickerJson}}'
    @endif
    class="overflow-hidden"
>
    <div
        @if(!edit)
        x-ref="strip"
        x-bind="strip"
        @endif
        class="flex w-max gap-8"
    >
        @dropzone("items", title: "Ticker Items")
    </div>
</div>
```

The whole interactive layer is gated behind `@if(!edit)`: in the canvas the ticker is a static, fully editable row. The config travels in a single-quoted `data-*` attribute, per the recommendation above.

```html
<!-- templates/alpine.html -->
@portal(bodyEnd, includeOnce: true, id: "com.example.ticker.alpine")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("exampleTicker", (id) => ({
            id,
            offset: 0,
            paused: false,
            frameId: null,
            lastTime: null,
            config: { speed: 60, pauseOnHover: true },

            init() {
                try {
                    Object.assign(this.config,
                        JSON.parse(this.$el.dataset.tickerConfig || "{}"));
                } catch (e) {
                    console.warn("Ticker " + this.id + ": invalid config JSON");
                }

                // Respect prefers-reduced-motion, including mid-session changes
                this.motionQuery = window.matchMedia("(prefers-reduced-motion: reduce)");
                this.onMotionChange = () =>
                    this.motionQuery.matches ? this.stop() : this.start();
                this.motionQuery.addEventListener("change", this.onMotionChange);

                // Restart cleanly after a back/forward-cache restore
                this.onPageShow = (event) => {
                    if (event.persisted) {
                        this.lastTime = null;
                        this.start();
                    }
                };
                window.addEventListener("pageshow", this.onPageShow);

                if (!this.motionQuery.matches) {
                    this.start();
                }
            },

            start() {
                if (this.frameId !== null || this.motionQuery.matches) return;
                this.frameId = requestAnimationFrame((t) => this.tick(t));
            },

            stop() {
                if (this.frameId !== null) {
                    cancelAnimationFrame(this.frameId);
                    this.frameId = null;
                }
                this.lastTime = null;
            },

            tick(time) {
                this.frameId = null;
                if (this.lastTime === null) this.lastTime = time;
                const elapsed = (time - this.lastTime) / 1000;
                this.lastTime = time;

                if (!this.paused) {
                    this.offset -= this.config.speed * elapsed;
                    const strip = this.$refs.strip;
                    // Fully scrolled out on the left? Re-enter from the right
                    if (strip && -this.offset >= strip.scrollWidth) {
                        this.offset = this.$el.clientWidth;
                    }
                }
                this.frameId = requestAnimationFrame((t) => this.tick(t));
            },

            destroy() {
                this.stop();
                this.motionQuery.removeEventListener("change", this.onMotionChange);
                window.removeEventListener("pageshow", this.onPageShow);
            },

            viewport: {
                ["@mouseenter"]() { if (this.config.pauseOnHover) this.paused = true; },
                ["@mouseleave"]() { this.paused = false; },
            },

            strip: {
                [":style"]() {
                    return { transform: "translateX(" + this.offset + "px)" };
                },
            },
        }));
    });
</script>
@endportal
```

The lifecycle concerns, one by one:

* **`init()` / `destroy()` symmetry** — every listener added in `init()` is removed in `destroy()`, and the animation frame is cancelled. Without this, removing the element leaks a window listener and an orphaned loop.
* **`requestAnimationFrame` with elapsed-time math** — movement is computed from real elapsed seconds (`speed` is pixels per second), so the ticker runs at the same visual speed on 60Hz and 144Hz displays, and survives dropped frames.
* **Pause on hover** — plain state (`paused = true`) rather than cancelling the loop, so resuming is instant and the elapsed-time math keeps the position continuous.
* **`prefers-reduced-motion`** — the loop never starts for users who asked for reduced motion, and the `change` listener honours the preference being toggled mid-session. The content remains fully visible and readable; only the motion is removed.
* **`pageshow` with `event.persisted`** — when a visitor navigates back to the page, browsers may restore it from the back/forward cache with your JavaScript frozen mid-flight. Resetting `lastTime` prevents one giant "catch-up" jump from the stale timestamp, and `start()` revives the loop if the browser dropped it.

The Content Slider's factory follows the same discipline at library scale: its `destroy()` calls `this.swiper.destroy()` so the Swiper instance is torn down with the element.

## Accessibility Driven by Bindings

Interactive widgets need the ARIA pattern that matches their behaviour, and Alpine's expression bindings are exactly the right tool: the ARIA state derives from the same reactive data that drives the visuals, so the two can never disagree. Tabs is the fullest example in the Core Pack. The markup declares the [tabs pattern](https://www.w3.org/WAI/ARIA/apg/patterns/tabs/) — `role="tablist"`, `role="tab"`, live `:aria-selected`, and a roving `:tabindex`:

```html
<!-- templates/index.html (Tabs) -->
<div
    class="{{classes.tabList}}"
    role="tablist"
    aria-label="Tabs"
>
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
            <!-- … icon and title spans elided … -->
        </button>
    @endeach
</div>
```

Each panel mirrors the relationship from the other side with `role="tabpanel"` and `:aria-labelledby="'tab-btn-' + '{{id}}' + '-' + {{ tab.index }}"`, so assistive technology can navigate button-to-panel in both directions. Because `activeTab` is the single source of truth, selecting a tab updates the visuals, `aria-selected`, and the tab order in one reactive sweep.

The keyboard interaction lives in the factory's `tabButton` binding group — arrow keys move focus *and* selection, `Home`/`End` jump to the extremes, and `.prevent` stops the page from scrolling:

```javascript
// templates/alpine.html (Tabs)
tabButton: {
    ["@click"]() {
        // … select the tab named by this button's data-tab-index …
    },
    ["@keydown.arrow-right.prevent"]() {
        const buttons = this.$el.parentElement.querySelectorAll("[role='tab']");
        const currentIndex = Array.from(buttons).indexOf(this.$el);
        const nextIndex = (currentIndex + 1) % buttons.length;
        buttons[nextIndex].focus();
        this.activeTab = nextIndex;
    },
    ["@keydown.arrow-left.prevent"]() {
        // … mirror of arrow-right, stepping backwards with wrap-around …
    },
    ["@keydown.home.prevent"]() {
        // … focus and select the first tab …
    },
    ["@keydown.end.prevent"]() {
        // … focus and select the last tab …
    },
},
```

The roving-tabindex trick deserves a highlight: only the active tab has `tabindex="0"`, every other tab sits at `-1`. A keyboard user Tab-keys once into the tab list, moves within it using arrow keys, then Tab-keys once to leave — instead of wading through every tab button on the way to the content. The handlers find their siblings with `querySelectorAll("[role='tab']")` scoped to the parent, so the same factory serves any number of tabs without configuration.

When you build your own interactive component, write the ARIA bindings at the same time as the visual ones. In the Tabs template they are literally adjacent attributes reading the same state — there is no cheaper moment to get accessibility right.

## Related Documentation

* [JavaScript Templates](../component/templates/js-templates.md) — property interpolation, quote-swap vs `data-*` configuration, and processing behaviour
* [The `@portal` Directive](../component/language/portal.md) — destinations, `includeOnce`, and deduplication IDs
* [`rw.setRootElement()`](../component/hooks.js/available-functions/rw.setrootelement.md) — building the root element that carries `x-data`
* [Modals, Overlays & Portals](modals-overlays-and-portals.md) — moving overlay markup with portals and wiring open/close triggers
* [Collection-Driven Dropzones](collection-driven-dropzones.md) — how Tabs turns a user-editable collection into the `tabItems` loop used here
