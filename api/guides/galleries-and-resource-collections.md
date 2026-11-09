---
description: Build media components around project resources, folders, and drag-and-drop
---

# Galleries & Resource Collections

Media components live or die on how well they handle *someone else's files*. You don't know how many images the user will add, what shape they'll be, whether captions exist, or whether one of them turns out to be a video. Elements' resource system absorbs all of that variability before your template runs: the user hands your component a folder, your hooks turn it into a clean array of ready-to-render items, and your template just loops. This guide walks that whole pipeline through a real component, then extends it with patterns for albums, metadata, and switchable layouts.

{% hint style="success" %}
This guide dissects the **Gallery** component (`com.realmacsoftware.gallery`) from the open-source [Core Pack](../development-resources/open-source-components.md). Open its source alongside this page.
{% endhint %}

## Resource Fundamentals, Briefly

[What are Resources?](../resource/what-are-resources.md) covers the ground rules, so here is just the working summary. A resource is any file the user has added to their project — image, video, audio, or an entire folder. Your component asks for one by declaring a [`resource` control](../component/properties.json/ui-controls/resource.md) in `properties.json`, and Elements delivers an object (not a bare URL) into `rw.props` and your templates: path, intrinsic dimensions, aspect ratio, alt text, format. Restrict what the control accepts with its `accepts`/`excludes` options if your component only handles certain types.

Two facts matter most for gallery-style components:

* **A folder is a single resource value.** Assign a folder and the property becomes a container whose `resources` field is an array of resource objects — one property in the inspector, arbitrarily many files behind it. See [Image Resources](../component/language/image-resources.md#folder-resources).
* **Any element can be a drop target.** Add `rwResourceDropZone="<control id>"` to an element in your template — or to your root element from hooks — and users can drag files from Finder or the Resources browser straight onto your component on the canvas.

## The Core Gallery, End to End

Gallery is the canonical resource-centric component: one folder in, a responsive thumbnail grid and a full-screen lightbox out. Everything it does flows from a single control in its `properties.json` — `{"title": "Resources", "id": "resources", "resource": {}}` — with no `accepts` restriction, because Gallery handles images and videos alike (you'll see how it tells them apart in a moment). The rest of its large inspector is pure presentation: columns, gap, aspect ratio, caption styling, lightbox chrome. The content side is this one dropwell.

### The Empty State Is the Drop Target

The first thing a user sees after dropping Gallery on the canvas is nothing — no folder assigned yet. Gallery's main template branches on that case immediately, and makes the placeholder itself the drop zone:

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

The `rwResourceDropZone="resources"` value matches the resource control's `id`, so a folder dragged onto the dashed box lands in the `resources` property and the whole component re-renders as a grid. The instruction and the target are the same element — users are never told to drop somewhere they can't.

Gallery scopes its drop zone to the empty state, but a component that stays droppable *after* content is assigned can wire the attribute onto its root element from hooks instead. The core Image component does exactly that, passing it through `rw.setRootElement`'s `args`:

```javascript
// com.realmacsoftware.image/hooks.source.js
const transformHook = (rw) => {
    // … link and class computation trimmed …
    rw.setRootElement({
        as: link.hasLink ? "a" : "div",
        class: classes.wrapper,
        args: {
            ...link.args,
            rwResourceDropZone: "image",
            id: globalID,
        },
    });
    // …
};

exports.transformHook = transformHook;
```

With that in place, dragging a new image anywhere onto the component replaces the current one — no need to hunt for the inspector.

### Processing the Folder in Hooks

Templates should loop and print, nothing more. All of Gallery's real work happens in `hooks.source.js`, which walks the folder's `resources` array once and enriches every item before the template sees it:

```javascript
// com.realmacsoftware.gallery/hooks.source.js
const transformHook = (rw) => {
    const {
        globalID,
        resources,
        lightboxPreview,
        // … ~50 presentation props trimmed …
    } = rw.props;
    // …

    const hasResources = resources?.resources?.length > 0;

    resources?.resources?.forEach((resource) => {
        resource.srcset = "";
        resource.thumbnail = rw.resizeResource(resource, 400);
        resource.alt = resource.alt || resource.caption || resource.author || "";

        // check if this is a video
        resource.isVideo =
            resource.format === "youtube" ||
            resource.format === "vimeo" ||
            resource.format === "mp4";

        // if it is a video, set booleans for isYoutube and isVimeo and isMP4
        if (resource.isVideo) {
            resource.isYouTube = resource.format === "youtube" ? true : false;
            resource.isVimeo = resource.format === "vimeo" ? true : false;
            resource.isMP4 = resource.format === "mp4" ? true : false;
            // … video captions and per-provider player options trimmed …
        }
    });

    // … class recipes and rw.setRootElement trimmed …

    rw.setProps({
        hasResources,
        classes,
        // … caption/author display booleans trimmed …
        resources: resources?.resources,
        edit: rw.project.mode === "edit",
        includeLightbox: lightboxPreview || rw.project.mode !== "edit",
        id: rw.node.id,
    });
};

exports.transformHook = transformHook;
```

Four moves worth internalising:

1. **`hasResources` is precomputed.** Template `@if` takes exactly one condition, so the length check lives here and the template tests a plain boolean. Every folder-driven component needs this line.
2. **Every item gets a thumbnail.** [`rw.resizeResource()`](../component/hooks.js/available-functions/rw.resizeresource.md) generates a 400px-wide variant per image and attaches its path to the item as `thumbnail`. Resizing at render time is impossible — templates can only read — so hooks are where scaled variants are born. For the full retina/`srcset`/per-breakpoint treatment, see [Responsive Images & Media](responsive-images-and-media.md).
3. **Alt text degrades gracefully.** `alt || caption || author || ""` means an image with no alt text still gets *something* descriptive, and the template never has to think about it.
4. **Format becomes booleans.** `resource.format` distinguishes videos (`youtube`, `vimeo`, `mp4`) from images, but rather than making the template compare strings — which `@if` can't do — the hook flattens the answer into `isVideo`, `isYouTube`, `isVimeo`, and `isMP4` flags the template can test directly.

Finally, `rw.setProps({ resources: resources?.resources })` promotes the *inner array* to a top-level prop, so the template writes `@each(image in resources)` instead of reaching through the container object.

### Rendering the Thumbnails

Back in `index.html`, the populated branch is one line — `@each(image in resources) @include("thumbnail") @endeach` — with the per-item markup extracted to an include. Includes share the scope of the template that includes them, so `thumbnail.html` can use the `image` loop variable and the `classes` prop directly:

```html
<!-- com.realmacsoftware.gallery/templates/include/thumbnail.html -->
<div
    @mouseenter="$dispatch('gallery-lightbox-scroll-to', {id: '{{id}}', index: {{image::index}}})"
    @click="$dispatch('gallery-lightbox-show', {id: '{{id}}', slide: {{image::index}}})"
    class="{{classes.thumbnail}}"
>
    @if(image.isVideo)
    <img src="{{image.image}}" alt="{{image.alt}}" class="{{classes.thumbnailImage}}" />
    @else
    <img src="{{image}}" alt="{{image.alt}}" class="{{classes.thumbnailImage}}" />
    @endif @if(thumbnailWantsMeta)
    <div class="{{classes.thumbnailMeta}}">
        @if (thumbnailShowCaption)
        <div class="{{classes.thumbnailCaption}}">{{image.caption}}</div>
        @endif @if (thumbnailShowAuthor)
        <div class="{{classes.thumbnailAuthor}}">{{image.author}}</div>
        @endif
    </div>
    @endif
</div>
```

Notice `src="{{image}}"` in the image branch: printing a resource object directly outputs its file path, so this renders the original file. The hook's 400px variant is on the same item as `{{image.thumbnail}}` whenever you want the scaled file instead — attach variants in hooks and each template decides which to print. The `{{image::index}}` loop variable (see [@each](../component/language/each.md#loop-variables)) rides along in the Alpine `$dispatch` calls, telling the lightbox which slide the clicked thumbnail corresponds to.

`thumbnailWantsMeta` is another precomputed boolean — the hook sets it to `thumbnailShowCaption || thumbnailShowAuthor`, an OR the template couldn't express itself.

### The Lightbox, Gated for the Canvas

The last line of `index.html` — `@includeIf(includeLightbox, template: "lightbox")` — decides whether the lightbox exists at all. Look back at the hook: `includeLightbox` is `lightboxPreview || rw.project.mode !== "edit"`. A fixed full-screen overlay would be hostile on the editing canvas, so by default it's only included outside edit mode; the inspector's Lightbox Preview switch opts back in so users can style it. The include itself teleports to the end of the page body and iterates the *same* processed array a second time:

```html
<!-- com.realmacsoftware.gallery/templates/include/lightbox.html -->
@portal("bodyEnd")
<div
    x-data="galleryLightbox('{{id}}')"
    @if(!edit)
    x-cloak
    @endif
    class="isolate fixed inset-0 z-50 flex w-full items-center justify-center pointer-events-none"
>
    <!-- … visibility bindings, overlay, nav buttons, and the scroll-snapping <ul> wrapper trimmed … -->
    @each(item in resources)
    <li class="{{classes.lightboxItem}}" @click="show = false" role="option">
        @includeIf(item.isYouTube, template: "youtube")
        @includeIf(item.isVimeo, template: "vimeo")
        @includeIf(item.isMP4, template: "mp4") @if(!item.isVideo)
        <img src="{{item}}" alt="{{item.alt}}"
            class="{{classes.lightboxItemMedia}} aspect-[{{item.aspect}}]" @click.stop />
        @endif
        <!-- … caption/author meta trimmed … -->
    </li>
    @endeach
</div>
@endportal
```

The video booleans computed in hooks pay off again — each `@includeIf` swaps in a provider-specific embed template, and images fall through to a plain `<img>` sized by the resource's own `aspect` field. The full story of mode gating (and why `x-cloak` sits inside `@if(!edit)`) is in [Designing the Edit-Mode Experience](edit-mode-experience.md#gating-heavy-behaviour-on-the-canvas).

## Albums from Nested Folders

A folder's `resources` array can contain folders. That one fact turns a flat gallery into an album browser: the user assigns a folder of folders, and each subfolder becomes an album with a name, a cover, and its own image set. A folder item carries a `resources` array of its own instead of an `image` field, which is exactly how a hook can tell the two apart. Here's a component we'll call `com.example.albums`, with a single resource control (`id: "library"`):

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { library } = rw.props;

    // A folder item carries a `resources` array instead of an `image` path.
    const albums = (library?.resources || [])
        .filter((item) => Array.isArray(item.resources))
        .map((folder) => {
            const images = folder.resources.filter((child) => child.image);
            return {
                name: folder.name,
                count: images.length,
                cover: images.length ? rw.resizeResource(images[0], 600) : null,
                images: images.map((image) => ({
                    src: rw.resizeResource(image, 800),
                    alt: image.alt || image.caption || "",
                })),
            };
        })
        .filter((album) => album.count > 0);

    rw.setProps({
        hasAlbums: albums.length > 0,
        albums,
    });
};
```

One pass builds everything the template needs: the first image in each subfolder becomes the album cover (resized to 600px), and every image gets an 800px display variant plus the same alt-fallback chain Gallery uses. The template renders a cover grid, then a detail section per album — the covers anchor-link down to their sections:

```html
<!-- templates/index.html -->
@if(hasAlbums)
<div class="grid grid-cols-2 gap-6 md:grid-cols-3">
    @each(album in albums)
    <a href="#album-{{album::index}}" class="group block">
        <img src="{{album.cover}}" alt="{{album.name}}" class="aspect-square w-full rounded-lg object-cover" />
        <p class="mt-2 font-medium">{{album.name}}</p>
        <p class="text-sm opacity-60">{{album.count}} photos</p>
    </a>
    @endeach
</div>

@each(album in albums)
<section id="album-{{album::index}}" class="mt-12">
    <h3 class="font-heading text-xl">{{album.name}}</h3>
    <div class="mt-4 grid grid-cols-3 gap-4">
        @each(image in album.images)
        <img src="{{image.src}}" alt="{{image.alt}}" class="rounded-lg" />
        @endeach
    </div>
</section>
@endeach
@endif
```

When `hasAlbums` is false, give the component the same `rwResourceDropZone` placeholder Gallery uses. The anchor-link detail view is deliberately the simplest sketch that works — to open albums in place instead, reuse the show/hide machinery from [Designing the Edit-Mode Experience](edit-mode-experience.md#keeping-hidden-content-editable); the data shape doesn't change, only the markup around `album.images`. And because the hook filters out empty albums and non-folder items, stray loose files in the user's folder are simply ignored rather than breaking the layout.

## Captions & Metadata

Every resource object carries a small, fixed set of descriptive fields. These are the ones documented in the references and used by the core Gallery — treat this as the complete menu:

| Field | Available on | Notes |
| ----- | ------------ | ----- |
| `image` | Images | Path to the image file |
| `path` | All files | Path for non-image files (video, audio, PDF) |
| `width` / `height` | Images | Intrinsic pixel dimensions |
| `aspect` | Images | Ratio string such as `16/9` — drops straight into `aspect-[…]` |
| `alt` | Images | Alt text set in the Resources browser |
| `format` | All files | File format token, e.g. `jpg`, `mp4`, `youtube` |
| `caption` / `author` | Folder items | Per-item metadata on resources inside a folder |
| `name` | Folders & items | The folder's or file's name |

Captions and authorship render like any other field — pair them in a `<figure>` and fall back gracefully when they're empty:

```html
@each(photo in shots.resources)
<figure>
    <img src="{{photo.image}}" alt="{{photo.alt}}" class="rounded-lg" />
    <figcaption class="mt-1 text-sm">{{photo.caption}} <span class="opacity-60">{{photo.author}}</span></figcaption>
</figure>
@endeach
```

Gallery's alt chain — `alt || caption || author || ""` — is the pattern to copy: compute the best available description once in hooks so templates never render an image with a missing `alt` attribute.

That's the extent of what Elements hands you. Richer metadata — camera EXIF, GPS, capture dates — isn't part of the resource object, and the hooks runtime has no module system to pull in a parser at run time. If you need it, bundle an EXIF library into your compiled `hooks.js` at build time and read the file yourself; [Integrating JavaScript Libraries](integrating-javascript-libraries.md) covers the bundling workflow.

## Switching Layout Engines

Once your hook owns all class generation (as Gallery's does with its `classes` object), offering multiple *layout engines* costs almost nothing: one inspector control, one branch in the hook, zero changes to the template. Here's a two-engine switcher — uniform grid versus CSS-columns masonry — driven by a [Segmented](../component/properties.json/ui-controls/segmented.md) control. `responsive: false` makes it return the raw item value rather than breakpoint-prefixed classes:

```json
{
  "title": "Layout",
  "id": "layoutEngine",
  "responsive": false,
  "segmented": {
    "default": "grid",
    "items": [
      { "value": "grid", "title": "Grid" },
      { "value": "columns", "title": "Masonry" }
    ]
  }
}
```

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { layoutEngine, gallery } = rw.props;
    const isMasonry = layoutEngine === "columns";

    // Grid crops to identical cells; CSS columns keep natural heights.
    const classes = {
        wrapper: isMasonry
            ? "columns-2 md:columns-3 gap-4"
            : "grid grid-cols-2 md:grid-cols-3 gap-4",
        item: isMasonry ? "mb-4 break-inside-avoid" : "aspect-square",
        image: isMasonry
            ? "w-full rounded-lg"
            : "h-full w-full rounded-lg object-cover",
    };

    rw.setProps({
        classes,
        hasImages: gallery?.resources?.length > 0,
    });
};
```

```html
<!-- templates/index.html -->
@if(hasImages)
<div class="{{classes.wrapper}}">
    @each(photo in gallery.resources)
    <div class="{{classes.item}}">
        <img src="{{photo.image}}" alt="{{photo.alt}}" class="{{classes.image}}" />
    </div>
    @endeach
</div>
@endif
```

The template is engine-agnostic: it prints `{{classes.wrapper}}`, `{{classes.item}}`, and `{{classes.image}}` and never knows which engine is active. Adding a third engine — say a JavaScript-measured masonry for perfectly packed layouts — is another branch in the hook and another segment in the control, with the same markup underneath. That's the property that keeps big media components maintainable as their inspectors grow.

## Related Documentation

* [What are Resources?](../resource/what-are-resources.md)
* [Working with Resources](../component/hooks.js/working-with-resources.md)
* [Image Resources](../component/language/image-resources.md)
* [Resource UI Control](../component/properties.json/ui-controls/resource.md)
* [Responsive Images & Media](responsive-images-and-media.md)
* [Designing the Edit-Mode Experience](edit-mode-experience.md)
