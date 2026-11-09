---
description: >-
  Combine responsive properties, theme breakpoints, and resizeResource to build
  responsive media components
---

# Responsive Images & Media

Serving one image file to every device wastes bandwidth on phones and looks soft on large retina displays. Elements gives you three separately-documented APIs that, combined, solve this properly: [`rw.responsiveProps`](../component/hooks.js/available-data/rw.getresponsivevalues.md) tells you what size the user wants at each breakpoint, [`rw.getBreakpoints()`](../component/hooks.js/available-functions/rw.getbreakpoints.md) tells you where those breakpoints sit in pixels, and [`rw.resizeResource()`](../component/hooks.js/available-functions/rw.resizeresource.md) manufactures an image file at any width you ask for. This guide shows how real components weave the three together — into `<picture>` elements, breakpoint-keyed class strings, and responsive background video.

{% hint style="success" %}
This guide dissects the **Image** (`com.realmacsoftware.image`), **Text Wrap** (`com.elementsplatform.shapes`), and **Container** (`com.realmacsoftware.container`) components from the open-source [Core Pack](../development-resources/open-source-components.md). Open their source alongside this page.
{% endhint %}

## The Three APIs

Each API answers one question, and none of them is useful for responsive media on its own:

| API | What it contributes | Shape |
| --- | --- | --- |
| [`rw.responsiveProps`](../component/hooks.js/available-data/rw.getresponsivevalues.md) | The user's per-breakpoint values for any responsive property control | `{ base: 400, md: 800, lg: 1200 }` — only explicitly set breakpoints appear |
| [`rw.theme.breakpoints`](../component/hooks.js/available-functions/rw.getbreakpoints.md) | The active theme's breakpoint names and pixel widths | `names: ["sm", "md", "lg", "xl", "2xl"]`, `screens: { sm: 640, md: 768, … }` |
| [`rw.resizeResource(resource, width)`](../component/hooks.js/available-functions/rw.resizeresource.md) | A resized variant of a project image resource | Returns a path string to the resized file |

The mental model: `rw.responsiveProps` holds *intent* ("400px wide on phones, 1200px on desktops"), `rw.theme.breakpoints` holds *geography* (where "phones" ends and "desktops" begins for this theme), and `rw.resizeResource` does the *manufacturing*. Your hook crosses intent with geography to decide which variants to manufacture, and your template emits them as `<source>` elements or class strings.

Two supporting facts shape everything below. First, every property control is responsive by default — for class-valued controls Elements prefixes Tailwind modifiers automatically, and you never touch these APIs (see [Responsive](../component/properties.json/general-structure/responsive.md)). You only reach for `rw.responsiveProps` when the raw per-breakpoint values need processing in hooks — a pixel width to resize by, a boolean to branch on. Second, `rw.resizeResource` takes a resource *object* (from a [resource control](../component/properties.json/ui-controls/resource.md)), not a URL — the full object structure is covered in [Working with Resources](../component/hooks.js/working-with-resources.md) and [Image Resources](../component/language/image-resources.md).

## Worked Example: The Core Image Component

The Image component's "Sizing" controls offer an **Original**/**Custom** choice (`imageSizingType`), and when the user picks Custom, a responsive **File Size** number control (`imageFileSize`, default 400) appears. Because that control stays responsive, the user can dial in a different pixel width at every breakpoint — and the hook turns each one into a real resized file.

The hook starts by gathering all three ingredients:

```javascript
// hooks.source.js (com.realmacsoftware.image) — excerpt
const {
    image,
    imageSizingType,
    // …
} = rw.props;

const {
    imageFileSize,
    // …
} = rw.responsiveProps;
const { breakpoints } = rw.theme;
const { names, screens } = breakpoints;

const wantsCustomSizing = imageSizingType == "custom";
```

Then it crosses `imageFileSize` with the theme's breakpoints to build one `<source>` descriptor per breakpoint the user actually configured:

```javascript
// hooks.source.js (com.realmacsoftware.image) — excerpt
const generateResourceSources = (resource) => {
    if (!wantsCustomSizing) return resource;

    const sources = names
        .filter((name) => imageFileSize[name])
        .sort((a, b) => screens[b] - screens[a])
        .map((name) => {
            const displayWidth = Math.min(imageFileSize[name], resource?.width || Infinity);
            const source = {
                media: `(min-width: ${screens[name]}px)`,
                srcset: rw.resizeResource(resource, imageFileSize[name] * 2),
                breakpoint: name,
                minWidth: screens[name],
            };
            if (resource?.width && resource?.height) {
                source.width = displayWidth;
                source.height = Math.round(displayWidth * resource.height / resource.width);
            }
            return source;
        });

    return {
        sources,
        fallbackSrc: resource,
        baseSrc: resource,
    };
};
```

Four details here are worth stealing:

* **Filter before you manufacture.** `.filter((name) => imageFileSize[name])` skips breakpoints the user never set — `rw.responsiveProps` only contains explicit values, so an untouched control produces just `{ base: 400 }` and exactly one variant.
* **Sort largest-first.** A browser walks `<source>` elements top to bottom and uses the *first* match. With `min-width` media queries, the widest query must come first, or a desktop browser would match the mobile source and stop. Every sources pipeline in this guide carries the same `.sort((a, b) => screens[b] - screens[a])`.
* **Double for retina.** `imageFileSize[name] * 2` requests a file at twice the display width, so the image stays sharp on HiDPI screens.
* **Report honest dimensions.** `Math.min(imageFileSize[name], resource?.width || Infinity)` clamps the *declared* width to the resource's intrinsic width, and the height is derived from the real aspect ratio — so the `width`/`height` attributes reserve the correct box and prevent layout shift.

A companion helper, `generateDefaultSrc`, does the same for the fallback `<img>`, resizing to `imageFileSize.base * 2` and clamping the declared dimensions the same way. The template then emits the whole structure as a `<picture>` element:

```html
<!-- templates/index.html (com.realmacsoftware.image) — excerpt -->
<picture class="{{classes.picture}}">
    <!-- … dark-mode sources trimmed … -->
    @each(source in lightImage.sources)
        <source
            media="{{source.media}}"
            srcset="{{source.srcset}}"
            @if(source.width)
            width="{{source.width}}"
            height="{{source.height}}"
            @endif
        />
    @endeach
    <!-- … lightbox sources trimmed … -->

    <!-- Fallback img element -->
    <img
        class="{{classes.img}}"
        src="{{lightImage.resource.image}}"
        alt="{{alt}}"
        width="{{imageWidth}}"
        height="{{imageHeight}}"
        decoding="async"
    />
</picture>
```

(The shipping template carries additional dark-mode sources, lightbox wiring, and image-protection attributes between these lines — trimmed here.) The division of labour is total: the template contains zero sizing logic. It loops whatever `sources` array the hook produced and falls back to a plain `<img>` for browsers — and breakpoints — that no `<source>` matched.

## Breakpoint-Keyed CSS and Class Generation

Automatic responsive prefixing works when a control's value *is* a Tailwind class. The core Text Wrap component (`com.elementsplatform.shapes`) — which floats media inside flowing text and wraps the text around the image's actual silhouette — hits the two cases where it can't work, and shows the manual escape hatch for each.

**Case one: the value can never be a class.** `shape-outside` takes a `url(…)` pointing at the image (often a `data:` URI holding encoded SVG). That string is unsafe as a Tailwind class name and would never exist in the compiled stylesheet anyway, so the hook builds an inline style instead:

```javascript
// hooks.source.js (com.elementsplatform.shapes) — excerpt
// Shape values (url(), polygon(), etc.) are unsafe as Tailwind class names
// and won't exist in the compiled CSS, so all shape CSS goes inline
const styles = [];

const shapeSourceUrl = isResourceMedia
    ? (isSvg ? svgImageUrl : media?.image)
    : externalSrc;

if (isImage && shapeSourceUrl && !opaqueRaster) {
    const threshold = (Number(shapeImageThreshold) || 0) / 100;
    // WebKit caches the extracted wrap shape by the shape-outside value and
    // won't recompute it on a threshold-only change, so vary the URL fragment
    const cacheKey = shapeSourceUrl.includes("#") ? `-rwt${threshold}` : `#rwt=${threshold}`;
    styles.push(`shape-outside: url('${shapeSourceUrl}${cacheKey}')`);
    styles.push(`shape-image-threshold: ${threshold}`);
}
// …
const mediaStyle = styles.length > 0 ? `${styles.join("; ")};` : "";
```

The template drops `{{mediaStyle}}` into a `style` attribute. Rule of thumb: dynamic values that Tailwind's compiler can't see at build time (URLs, computed numbers, user-entered strings) become inline CSS; everything else stays a class.

**Case two: the class depends on *another* value at the same breakpoint.** Which margin side gets a class depends on which way the media floats — and both float side and margin are responsive. The hook resolves each per breakpoint, using a helper that reimplements the mobile-first cascade over the sparse `rw.responsiveProps` object:

```javascript
// hooks.source.js (com.elementsplatform.shapes) — excerpt
const resolveResponsiveValue = (breakpoints, values, bp, fallback) => {
    const index = breakpoints.indexOf(bp);

    for (let i = index; i >= 0; i--) {
        const value = values[breakpoints[i]];
        if (value !== undefined && value !== null) {
            return value;
        }
    }

    return fallback;
};

const withBreakpointPrefix = (breakpoint, className) => {
    // …
    return breakpoint === "base" ? className : `${breakpoint}:${className}`;
};
```

Because `rw.responsiveProps` only contains explicitly set breakpoints, `resolveResponsiveValue` walks *downward* from the requested breakpoint until it finds a value — exactly how min-width media queries inherit in CSS. With those two helpers, the main routine iterates `["base", ...names]`, resolves float and margin at each stop, and emits prefixed classes only where something changed:

```javascript
// hooks.source.js (com.elementsplatform.shapes) — excerpt, trimmed
const getFloatMarginClasses = (floatByBp, marginByBp, breakpointNames) => {
    const breakpoints = ["base", ...breakpointNames];
    const classes = [];
    let prevFloat = null;
    // …

    for (const bp of breakpoints) {
        const float = resolveFloat(bp);
        const margin = resolveMargin(bp);
        // …

        if (float === "left") {
            const mrClass = marginTokenToClass("mr", margin);
            if (mrClass) {
                classes.push(withBreakpointPrefix(bp, mrClass));
            }
            if (prevFloat === "right") {
                classes.push(withBreakpointPrefix(bp, "ml-0"));
            }
        }
        // … (mirror-image "right" and "none" branches trimmed)

        prevFloat = float;
        // …
    }

    return classes.filter(Boolean).join(" ");
};

const { mediaFloat: floatByBp } = rw.responsiveProps || {};
const { names: breakpointNames = [] } = rw.theme?.breakpoints || {};
const floatMarginClasses = getFloatMarginClasses(
    floatByBp || {},
    marginByBreakpointFromFormatted(shapeMargin),
    breakpointNames
);
```

Note the `prevFloat` tracking: when the float side flips from right to left at some breakpoint, the hook must both add the new `mr-*` margin *and* zero out the old one with `ml-0` — the kind of pairwise dependency automatic prefixing can never express. The result is an ordinary class string (`mr-4 mb-4 md:mr-0 md:ml-6 …`) merged into the media element's class list.

## Scaling It Up: A Responsive Card Image

The same crossing generalises to any component that renders images at a user-controlled size. Here is a compact `com.example.cardImage` that exposes one responsive **Thumbnail Width** control and builds a full breakpoint-to-variant map from it. The control is a plain number — responsive by default, so no extra configuration is needed:

```json
{
    "title": "Thumbnail Width",
    "id": "thumbWidth",
    "number": { "default": 400, "round": true, "subtitle": "In pixels" }
}
```

```javascript
// hooks.js — com.example.cardImage
const transformHook = (rw) => {
    const { photo, caption } = rw.props;
    const { thumbWidth } = rw.responsiveProps;
    const { names, screens } = rw.theme.breakpoints;

    const hasPhoto = !!photo?.image;
    if (!hasPhoto) {
        rw.setProps({ hasPhoto });
        return;
    }

    // Cross the user's responsive width with every theme breakpoint:
    // each breakpoint with an explicit value gets its own resized variant.
    const sources = names
        .filter((name) => thumbWidth[name] && screens[name])
        .sort((a, b) => screens[b] - screens[a])
        .map((name) => ({
            media: `(min-width: ${screens[name]}px)`,
            srcset: rw.resizeResource(photo, thumbWidth[name] * 2),
            width: Math.min(thumbWidth[name], photo.width || Infinity),
        }));

    const baseWidth = thumbWidth.base || 400;

    rw.setProps({
        hasPhoto,
        sources,
        fallbackSrc: rw.resizeResource(photo, baseWidth * 2),
        fallbackWidth: Math.min(baseWidth, photo.width || Infinity),
        alt: photo.alt || caption || "",
        aspect: photo.aspect,
    });
};

exports.transformHook = transformHook;
```

```html
<!-- templates/index.html -->
@if(hasPhoto)
    <figure>
        <picture>
            @each(source in sources)
                <source media="{{source.media}}" srcset="{{source.srcset}}" width="{{source.width}}" />
            @endeach
            <img
                src="{{fallbackSrc}}"
                alt="{{alt}}"
                width="{{fallbackWidth}}"
                style="aspect-ratio: {{aspect}}"
                loading="lazy"
                decoding="async"
            />
        </picture>
        <figcaption>{{caption}}</figcaption>
    </figure>
@endif
```

If the user leaves the control alone, `thumbWidth` is `{ base: 400 }`, the `sources` array is empty, and the component ships a single 800px file. The moment they set a width at `md` and `lg`, two `<source>` variants appear — no template changes, no new controls. To scale this across a whole gallery, run the same `sources`-building function once per resource inside a map over the collection (see [Galleries & Resource Collections](galleries-and-resource-collections.md)) — but read the variant-cost pitfall below first.

## Responsive Background Video

Video can't be resized the way images can, so the core Container component makes its background video responsive with a different toolkit: fill-the-box CSS plus per-format template selection. The hook reduces the video resource's `format` field to one boolean per embed mechanism — precomputed because [`@if`](../component/language/if.md) and [`@includeIf`](../component/language/includeif.md) take a single condition:

```javascript
// hooks.source.js (com.realmacsoftware.container) — excerpt
const bgVideo =
    globalBgType == "video" && globalBgVideo
        ? {
            isYoutube: globalBgVideo.format == "youtube",
            isVimeo: globalBgVideo.format == "vimeo",
            isMP4: globalBgVideo.format == "mp4",
            video: globalBgVideo,
        }
        : false;
```

The template then picks exactly one partial per format with `@includeIf`:

```html
<!-- templates/index.html (com.realmacsoftware.container) — excerpt -->
<div class="{{classes.background}}">
    @if(hasBgVideo)
        <div class="fixed w-full h-full">
            @includeIf(bgVideo.isYoutube, template:"youtube")
            @includeIf(bgVideo.isVimeo, template:"vimeo")
            @includeIf(bgVideo.isMP4, template:"mp4")
        </div>
    @endif
</div>
```

Each partial in `templates/include/` renders its own embed markup. The MP4 one is the simplest:

```html
<!-- templates/include/mp4.html (com.realmacsoftware.container) -->
<video
    class="w-full h-full object-cover"
    preload="auto"
    muted="muted"
    loop="loop"
    autoplay="autoplay"
    playsinline
    webkit-playsinline
>
    <source src="{{bgVideo.video.path}}" type="video/mp4" />
    Your browser does not support the video tag.
</video>
```

The responsiveness lives entirely in `w-full h-full object-cover`: the video fills whatever box the container occupies at any viewport and crops overflow, so no per-breakpoint variants are needed. Note the video file arrives via `bgVideo.video.path` — the `path` field, not `image`, is how non-image resources expose their file (see [Image Resources](../component/language/image-resources.md)) — and the autoplay attributes (`muted`, `playsinline`) are exactly the set mobile browsers require before they'll autoplay anything.

## Pitfalls

**`rw.resizeResource` works on project resources, not URLs.** Its first parameter is an image resource object from your properties or collections — a pasted remote URL or a CMS field token has no local file to resize. The core Image component respects this split: only `imageType == "resource"` images flow through `generateResourceSources`; custom-URL and CMS images pass their per-breakpoint URL strings straight through to `<source>` elements unresized.

**Get the `<source>` order and media queries right.** The browser commits to the first matching `<source>`, so `min-width` queries must be sorted widest-first, and the query should describe the *layout* breakpoint, not the image. If your card sits in a three-column grid above `lg`, the image displayed there is roughly a third of the viewport — size the `lg` variant for the rendered slot, not the full screen width. Declared `width`/`height` attributes should describe display size, clamped to the resource's intrinsic width, or you'll reserve the wrong box and cause layout shift.

**Every variant is a manufactured file.** Each distinct `rw.resizeResource(resource, width)` call produces an image at export. One hero image across five breakpoints is six files; a 60-image gallery crossed with five breakpoints is hundreds. Follow the core Image's lead: filter to breakpoints the user explicitly set, and for galleries consider one shared variant width per breakpoint rather than per-image sizing.

**Edit mode changes what you have to work with.** CMS field tokens can't resolve inside the editor, so both Image and Text Wrap swap in a shared placeholder (`${sharedAssetPath}/images/image-square.png`) when `rw.project.mode` is `"edit"`, and Image disables its lightbox there entirely. Check the mode before wiring behaviour that only makes sense on a published page — [Designing the Edit-Mode Experience](edit-mode-experience.md) covers the full pattern.

## Related Documentation

* [Working with Resources](../component/hooks.js/working-with-resources.md)
* [rw.resizeResource()](../component/hooks.js/available-functions/rw.resizeresource.md)
* [rw.getBreakpoints()](../component/hooks.js/available-functions/rw.getbreakpoints.md)
* [rw.responsiveProps](../component/hooks.js/available-data/rw.getresponsivevalues.md)
* [Responsive Properties](../component/properties.json/general-structure/responsive.md)
* [Image Resources](../component/language/image-resources.md)
* [Galleries & Resource Collections](galleries-and-resource-collections.md)
