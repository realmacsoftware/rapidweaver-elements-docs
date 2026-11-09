---
description: Ship third-party JavaScript libraries with your components
---

# Integrating JavaScript Libraries

Sooner or later a component needs more JavaScript than you want to write yourself — a carousel engine, a lightbox, a scroll-animation library, a physics engine. The question is never *whether* you can use a third-party library in Elements; it's the three questions that follow: where do the library files live, how does the library load **exactly once** no matter how many components depend on it, and how does each component instance bind to the single loaded copy? This guide answers all three, then covers the special case of using an npm library inside `hooks.js`, where there is no module system at all.

{% hint style="success" %}
This guide dissects the **Reveal** (`com.realmacsoftware.reveal`) and **Gallery** (`com.realmacsoftware.gallery`) components from the open-source [Core Pack](../development-resources/open-source-components.md). Open their source alongside this page.
{% endhint %}

## Where Library Files Live

A library file has three possible homes, and the choice shapes everything downstream — how you reference it, how many copies ship, and what happens on publish:

| Location | Deployed | Referenced with | Best when |
|----------|----------|-----------------|-----------|
| Component `assets/page/` | Once per publish, into the page's files directory | `{{assetPath}}` — a prop you set from `rw.component.assetPath` in `hooks.js` | Exactly one component needs the library |
| Pack `shared/assets/` | Once per pack | `{{assetPath}}` (automatic) in shared templates; `rw.component.sharedAssetPath` from hooks | Several components in your pack share the library |
| CDN | Not deployed — loaded from a third-party server | An absolute URL inside a portal | Prototyping, or libraries whose license forbids redistribution |

The trade-offs pull in different directions. **Component-level assets** keep the library scoped to the one component that needs it, but if three of your components each vendor the same carousel engine, three copies ship — and unless all three deduplicate their loaders with the same portal `id`, three copies load. **Pack-level shared assets** hold one copy for the whole pack, but a library referenced from a [shared template](../component/shared-files/templates.md) loads on *every* page that uses *any* component from your pack, whether that page needs it or not. **CDNs** add zero weight to your pack but make every published site depend on a third-party server — more on that [below](#loading-from-a-cdn).

{% hint style="info" %}
`{{assetPath}}` is one spelling with two meanings. Inside a **shared template**, it resolves automatically to your pack's `shared/assets/` folder — see [Shared Assets](../component/shared-files/assets.md). Inside a **component template**, nothing is automatic: it's an ordinary prop you must set yourself from [`rw.component`](../component/hooks.js/available-data/rw.element.md), and you can name it anything — the Core Pack's Content Slider calls it `componentAssetPath` to avoid ambiguity.
{% endhint %}

This is exactly how the Core Pack organises its own dependencies. Its `shared/assets/` folder carries the libraries that many core components lean on:

```
shared/assets/  (Core Pack)
├── alpine.js               # Alpine v3 core
├── alpine-collapse.js      # …plus official Alpine plugins
├── alpine-focus.js
├── alpine-intersect.js
├── alpine-ui.js
├── gsap.min.js             # GSAP core
├── ScrollTrigger.min.js    # GSAP scroll plugin
├── gsap-effects.js         # Realmac's registered GSAP effects
├── image-lightbox.js       # a shared Alpine factory (see below)
├── smoothscroll.min.js
└── …
```

Meanwhile the Content Slider — the only core component that needs Swiper — vendors `swiper-bundle.min.js` and `swiper-bundle.min.css` in its own `assets/page/` folder. One library, one consumer, component-level; one library, many consumers, pack-level. Remember that `page` is the only supported subfolder for component assets — see [Assets](../component/assets.md).

## Loading a Library Exactly Once

There are two mechanisms for getting a `<script>` tag onto the page a single time, and they differ in *when* the cost is paid.

### Pack-Shared Templates

Files in `shared/templates/headStart|headEnd|bodyStart|bodyEnd/` are injected automatically, **once per page per pack**, whenever any component from your pack appears on that page — no portal, no `includeOnce`, no opt-in from individual components. This is how the Core Pack puts GSAP and Alpine on every page:

```html
<!-- shared/templates/headStart/setup.html (Core Pack) -->
<script defer src="{{assetPath}}/alpine-collapse.js"></script>
<script defer src="{{assetPath}}/alpine-focus.js"></script>
<script defer src="{{assetPath}}/alpine-intersect.js"></script>
<script defer src="{{assetPath}}/alpine-ui.js"></script>
<script defer src="{{assetPath}}/alpine.js"></script>
<script src="{{assetPath}}/smoothscroll.min.js"></script>
<script src="{{assetPath}}/gsap.min.js"></script>
<script src="{{assetPath}}/ScrollTrigger.min.js"></script>
<script src="{{assetPath}}/gsap-effects.js"></script>
```

A second shared template at the other end of the document consumes what the first one loaded. This is the Reveal system's engine — a single script, once per page, that wires GSAP's ScrollTrigger to every reveal-enabled element:

```html
<!-- shared/templates/bodyEnd/reveal.html (Core Pack) -->
<script>
    gsap.registerPlugin(ScrollTrigger);
    document.addEventListener("DOMContentLoaded", () => {
        const revealElements = document.querySelectorAll("[data-reveal]");
        revealElements.forEach((element, index) => {
            const {
                revealAnimation: animation = "fadeUpIn",
                revealStart: start = "top bottom",
                revealDuration: duration = 0.5,
                // … further data-reveal-* options elided …
            } = element.dataset;
            // … build a ScrollTrigger config and play gsap.effects[animation] …
        });
    });
</script>
```

Note the position pairing: the library loads in `headStart` (so it exists before anything else runs), the consumer sits in `bodyEnd` (so the DOM exists before it queries). The [shared templates reference](../component/shared-files/templates.md) documents all four injection points.

The cost of this convenience: every page that uses even one trivial component from your pack carries every library your shared templates load. Reserve shared templates for libraries most of your pack genuinely needs — the Core Pack can justify page-wide GSAP because dozens of its components use it.

### Per-Component Portals with includeOnce

When only one or two components need a library, load it from the component's own template with [`@portal`](../component/language/portal.md), and make the portal deduplicate itself:

```html
<!-- templates/alpine.html (Content Slider) -->
@portal(bodyEnd, id: "com.realmacsoftware.contentSlider.script", includeOnce: true)
<script src="{{componentAssetPath}}/swiper-bundle.min.js"></script>
<script>
    // … registers the elementsContentSlider factory on alpine:init …
</script>
@endportal
```

Two rules are non-negotiable. First, **any portal containing a `<script>` needs `includeOnce: true` and a reverse-DNS `id`** — without them, ten sliders on a page emit ten copies of Swiper. Second, if two *different* components vendor the same library, give both loader portals the **same** `id` so the page gets one copy regardless of which components appear. And because an `includeOnce` portal is emitted for the first instance only, never interpolate per-instance property values inside one — the [Alpine guide](interactive-components-with-alpine.md#shipping-styles-through-portals) explains the failure mode.

The economics are the inverse of shared templates: the library costs nothing on pages that don't use the component, and exactly one copy on pages that do.

## Binding Instances After the Library Loads

A loaded library is inert until something calls it — and that something must run *after* the library exists. The core components use two sequencing patterns, chosen by whether the library is plain JavaScript or Alpine-based.

### Plain Libraries: DOMContentLoaded Plus data-\* Attributes

Reveal never runs GSAP code per instance. Instead, each instance's `hooks.js` publishes its configuration as `data-reveal-*` attributes on the root element — the `globalReveal` helper from [rw-elements-tools](../development-resources/build-tools/README.md) computes them from the component's properties:

```javascript
// hooks.source.js (Reveal)
const reveal = globalReveal(rw);

rw.setRootElement({
    as: globalHTMLTag(rw, "div"),
    class: classes,
    args: {
        ...reveal,
    }
});
```

The once-per-page `reveal.html` script you saw above does the rest: on `DOMContentLoaded` it queries `[data-reveal]`, reads each element's `dataset`, and builds the ScrollTrigger animations. The instances and the library never touch — instances publish data, the single consumer script reads it. This decoupling is why the pattern scales: adding an eleventh reveal-enabled element adds eleven attributes to the page, not another script.

### Alpine Factories: alpine:init Plus Events Keyed by ID

For Alpine-based integration the sequencing event is `alpine:init`, which fires after Alpine loads but before it scans the page for `x-data`. The Gallery's lightbox is the full worked example. Its factory registers once through a deduplicated portal:

```html
<!-- templates/alpine-gallery-lightbox.html (Gallery) -->
@portal("bodyEnd", id: "com.realmacsoftware.alpine.gallery-lightbox",
includeOnce: true)
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("galleryLightbox", (id = null, options = {}) => ({
            id,
            // … state, init(), and keyboard controls elided …
            setupEventListeners() {
                // … gallery-lightbox-scroll-to listener elided …
                window.addEventListener("gallery-lightbox-show", (event) => {
                    if (this.id === event.detail.id) {
                        this.show = true;
                        this.scrollTarget = event.detail.slide;
                    }
                });
                // … $watch on show elided …
            },
            // … navigation methods and binding groups elided …
        }));
    });
</script>
@endportal
```

Each Gallery instance then connects itself to the shared factory by passing its own ID into `x-data`, and its thumbnails talk to the lightbox through events that carry the same ID:

```html
<!-- templates/include/lightbox.html (Gallery) -->
@portal("bodyEnd")
<div
    x-data="galleryLightbox('{{id}}')"
    @if(!edit)
    x-cloak
    @endif
    class="isolate fixed inset-0 z-50 flex w-full items-center justify-center pointer-events-none"
>
    <!-- … overlay, close button, slide list, and nav buttons elided … -->
</div>
@endportal
```

(The transition and `x-effect` attributes on the wrapper are elided here.) Note the lightbox markup itself also travels through a portal to `bodyEnd` — a separate overlay-positioning concern covered in [Modals, Overlays & Portals](modals-overlays-and-portals.md).

```html
<!-- templates/include/thumbnail.html (Gallery) -->
<div
    @mouseenter="$dispatch('gallery-lightbox-scroll-to', {id: '{{id}}', index: {{image::index}}})"
    @click="$dispatch('gallery-lightbox-show', {id: '{{id}}', slide: {{image::index}}})"
    class="{{classes.thumbnail}}"
>
```

The factory filters every event against `this.id`, so five galleries on one page stay independent while sharing one copy of the logic. When a factory serves *multiple components* rather than multiple instances of one, promote it to a shared asset: the Core Pack's `shared/assets/image-lightbox.js` registers an `imageLightbox` factory the same way — `document.addEventListener("alpine:init", () => { Alpine.data("imageLightbox", (id) => ({ … })) })` — and is loaded once per page by a shared `headEnd` template, ready for any component that wants a lightbox. The factory mechanics themselves are covered in depth in [Interactive Components with Alpine.js](interactive-components-with-alpine.md#the-factory-pattern).

## A Complete Worked Pattern: Vendoring a Carousel

Here is the whole technique in one generic component, `com.example.carousel`, wrapping an invented library whose API is `window.Carousel.create(el, options)`. The files:

```
com.example.carousel/
├── assets/
│   └── page/
│       ├── carousel.min.js
│       └── carousel.min.css
├── hooks.js
└── templates/
    ├── index.html
    └── carousel.html
```

The hook exposes the asset path and packages the instance configuration as JSON:

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { autoplay, interval, loop } = rw.props;
    const { id } = rw.node;

    rw.setProps({
        id,
        edit: rw.project.mode === "edit",
        assetPath: rw.component.assetPath,
        carouselJson: JSON.stringify({
            autoplay: autoplay === true || autoplay === "true",
            interval: Number(interval) || 5000,
            loop: loop === true || loop === "true",
        }),
    });
};
```

The markup carries the per-instance config in a single-quoted `data-*` attribute and stays completely inert in the edit canvas:

```html
<!-- templates/index.html -->
@include("carousel")

<div
    @if(!edit)
    x-data="exampleCarousel('{{id}}')"
    data-carousel-config='{{carouselJson}}'
    @endif
    class="example-carousel"
>
    @dropzone("slides", title: "Slides")
</div>
```

And one template file owns the component's entire page-level footprint — stylesheet to the head, library plus factory to the end of the body, everything deduplicated:

```html
<!-- templates/carousel.html -->
@portal(headEnd, id: "com.example.carousel.styles", includeOnce: true)
<link rel="stylesheet" href="{{assetPath}}/carousel.min.css">
@endportal

@portal(bodyEnd, id: "com.example.carousel.script", includeOnce: true)
<script src="{{assetPath}}/carousel.min.js"></script>
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("exampleCarousel", (id) => ({
            id,
            carousel: null,

            init() {
                let options = {};
                try {
                    options = JSON.parse(this.$el.dataset.carouselConfig || "{}");
                } catch (e) {
                    console.warn("Carousel " + this.id + ": invalid config JSON");
                }
                this.carousel = window.Carousel.create(this.$el, options);
            },

            destroy() {
                if (this.carousel) {
                    this.carousel.destroy();
                    this.carousel = null;
                }
            },
        }));
    });
</script>
@endportal
```

Every moving part earns its place: the library `<script>` sits *inside* the same `includeOnce` portal as the factory, so they load together or not at all and their order is guaranteed; the factory reads its options back from `data-carousel-config` in `init()`, so per-instance values never leak into the once-only portal; and `destroy()` tears the library instance down when Alpine removes the element, mirroring how the Core Pack's Content Slider calls `this.swiper.destroy()`.

## Loading from a CDN

Sometimes vendoring isn't an option — the library's license forbids redistribution, or you're prototyping and don't want to manage files yet. A CDN load uses the same portal discipline, with a **pinned version** in the URL:

```html
@portal(bodyEnd, id: "com.example.charts.library", includeOnce: true)
<script defer src="https://cdn.example.com/chartlib@4.2.1/chart.min.js"></script>
@endportal
```

{% hint style="warning" %}
A CDN reference makes every published site depend on a server neither you nor your users control. If the CDN is down, blocked (corporate networks, some countries), or the URL scheme changes, the published site breaks — and the site owner will blame the component. Pin exact versions (never `@latest`, which can ship breaking changes into live sites), and remember the privacy angle: every visitor's browser contacts the third-party host, which may need disclosure under privacy regulations. For anything you sell, vendored assets are the reliable default.
{% endhint %}

## Using Libraries Inside hooks.js

Everything so far ships libraries to the *published page*. Using a library inside `hooks.js` — at build time, while Elements renders your component — is a different problem, because the hooks runtime has **no module system**: no `require`, no `import`, no npm resolution. A `hooks.js` file must be entirely self-contained.

The way to use an npm package anyway is a pre-build step that bundles it *into* `hooks.js`. This fits the convention you'll already have from [rw-elements-tools](../development-resources/build-tools/README.md): you author `hooks.source.js`, a compile step produces the `hooks.js` that ships, and both files sit side by side in the component (as they do throughout the Core Pack). Suppose your source uses a hypothetical `slugify` package:

```javascript
// hooks.source.js — authored with npm imports; never executed by Elements
const slugify = require("slugify");

exports.transformHook = (rw) => {
    const { heading } = rw.props;

    rw.setProps({
        anchorSlug: slugify(String(heading || ""), { lower: true }),
    });
};
```

One esbuild invocation inlines the entire package and emits a self-contained file:

```json
{
  "scripts": {
    "build:hooks": "esbuild components/com.example.anchor/hooks.source.js --bundle --format=cjs --platform=neutral --outfile=components/com.example.anchor/hooks.js"
  }
}
```

```bash
npm install --save-dev esbuild slugify
npm run build:hooks
```

The generated `hooks.js` contains the full `slugify` implementation followed by your unchanged `transformHook` — no imports left, nothing to resolve at run time. Re-run the script whenever the source changes, and treat the output as generated code.

Two constraints to respect. First, the Elements hooks runtime is a plain JavaScript sandbox: no `window`, no `document`, and no Node globals (`process`, `Buffer`, `fs`, timers). Prefer pure-computation libraries — slug generators, parsers, formatters, hash functions. `--platform=neutral` keeps esbuild from assuming either environment, but it won't save a library that probes for `process` at load time; for those, either define minimal stubs ahead of the bundled code or pick a dependency-free alternative. Second, bundle per component — each `hooks.js` stands alone, so a package shared by three components is inlined three times. That's the correct trade: build-time file size is cheap, a broken runtime resolution is not.

## Live Preview on the Editing Canvas

Page-level library loaders do not run on the canvas. To show a Three.js (or other ES-module) scene while the user edits, emit an `rwlivepreview` tag in edit mode and export `mount` / `update` / `dispose` from an editor-only module. The editor imports that module, owns lifecycle, and resolves `import * as THREE from 'three'` to a shared copy. See [Editor Live Preview](editor-live-preview.md).

## Cleanup and Lifecycle Hygiene

A library instance you create is a library instance you own. Give every Alpine factory that wraps a library a `destroy()` that mirrors its `init()` — tear down the instance, cancel animation loops, and remove any `window`-level listeners you added, or removed components leak them. Restore state on `pageshow` when `event.persisted` is true, because browsers revive pages from the back/forward cache with your JavaScript frozen mid-flight. And gate motion-heavy libraries behind `prefers-reduced-motion`, honouring changes mid-session. The [ticker example](interactive-components-with-alpine.md#a-self-contained-animation-component) in the Alpine guide demonstrates the complete checklist line by line — every library integration you ship should pass it.

## Related Documentation

* [Assets](../component/assets.md) — component-level `assets/page/` and the `{{assetPath}}` hook wiring
* [Shared Assets](../component/shared-files/assets.md) — pack-level asset storage and referencing
* [Shared Templates](../component/shared-files/templates.md) — the four injection points and once-per-page behaviour
* [The `@portal` Directive](../component/language/portal.md) — destinations, `includeOnce`, and deduplication IDs
* [Interactive Components with Alpine.js](interactive-components-with-alpine.md) — the factory pattern, configuration passing, and lifecycle discipline
* [Editor Live Preview](editor-live-preview.md) — running Three.js and other ES modules on the editing canvas
* [Build Tools](../development-resources/build-tools/README.md) — the `hooks.source.js` → `hooks.js` workflow and shared hooks like `globalReveal`
