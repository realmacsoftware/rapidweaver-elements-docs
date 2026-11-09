---
description: Reading image and folder resources in your templates — paths, dimensions, alt text, and hook-resized variants
---

# Image Resources

When a user assigns an image to a [resource control](../properties.json/ui-controls/resource.md), your template doesn't receive a bare URL — it receives a resource object carrying the path plus everything you need to render the image well: intrinsic dimensions, aspect ratio, and alt text. This page covers how to read those fields in templates, how folder resources work, and how resized variants generated in hooks reach your markup.

## What a Resource Exposes to Templates

For a resource control with the id `photo`, these fields are available anywhere in your templates:

| Field | Description |
| ----- | ----------- |
| `{{photo.image}}` | The URL/path to the image file |
| `{{photo.path}}` | The file path — use this for non-image files such as video, audio, or PDFs |
| `{{photo.width}}` | Intrinsic width in pixels (images only) |
| `{{photo.height}}` | Intrinsic height in pixels (images only) |
| `{{photo.aspect}}` | Aspect ratio string such as `16/9` (images only) |
| `{{photo.alt}}` | The alt text set in the Resources browser |
| `{{photo.format}}` | The file format, such as `jpg` |

A resource control with nothing assigned yields no `image` value, so guard your markup — `@if` takes a single condition, and a field lookup works as one:

```html
@if(photo.image)
  <img
    src="{{photo.image}}"
    alt="{{photo.alt}}"
    width="{{photo.width}}"
    height="{{photo.height}}"
  />
@endif
```

Writing `width` and `height` from the resource's intrinsic dimensions prevents layout shift while the image loads, and `{{photo.aspect}}` slots straight into an `aspect-ratio` CSS value. The core Image component leans on exactly these fields — its hooks read `image.alt`, `image.aspect`, `image.width`, and `image.height` to size and describe its `<picture>` element.

## Folder Resources

When the user assigns a **folder** of resources instead of a single file, the property becomes a container object: its `name` is the folder's name, and its `resources` field is an array of resource objects, each carrying the same fields as above plus per-item `caption` and `author` metadata. Iterate the array with [`@each`](each.md):

```html
@if(hasPhotos)
  <div class="grid grid-cols-3 gap-4">
    @each(photo in gallery.resources)
      <figure>
        <img src="{{photo.image}}" alt="{{photo.alt}}" />
        <figcaption>{{photo.caption}}</figcaption>
      </figure>
    @endeach
  </div>
@endif
```

The `hasPhotos` boolean comes from hooks — precompute it there rather than testing a length in the template:

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { gallery } = rw.props;

    rw.setProps({
        hasPhotos: gallery?.resources?.length > 0,
    });
};
```

This is the pattern the core Gallery component uses: one folder resource in the inspector, `resources?.resources?.length > 0` computed in hooks, and an `@each` over the items in the template. Folder items also expose `format`, which Gallery checks to tell videos (`youtube`, `vimeo`, `mp4`) apart from images.

## Resized Variants from Hooks

Templates can only read what they're given, so image processing happens in `hooks.js`. Call [`rw.resizeResource()`](../hooks.js/available-functions/rw.resizeresource.md) to generate scaled versions, then hand the resulting paths to the template with `rw.setProps()`:

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { photo } = rw.props;
    const hasPhoto = Boolean(photo && photo.image);

    rw.setProps({
        hasPhoto,
        thumbnail: hasPhoto ? rw.resizeResource(photo, 800) : null,
        fullsize: hasPhoto ? photo.image : null,
    });
};
```

```html
@if(hasPhoto)
  <a href="{{fullsize}}"><img src="{{thumbnail}}" alt="{{photo.alt}}" /></a>
@endif
```

Because `setProps` accepts arrays and nested objects, hooks can pass an entire set of per-breakpoint sources and let the template loop over them. The core Image component builds each `srcset` entry with `rw.resizeResource()` in its hooks, then renders them like this:

```html
<!-- com.realmacsoftware.image/templates/index.html -->
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
```

## Drag-and-Drop Targets

Adding `rwResourceDropZone="photo"` (the value being your resource control's `id`) to an element in your template turns it into a canvas drop target, so users can drag an image straight onto your component — see the [Resource control reference](../properties.json/ui-controls/resource.md#resource-dropzones).

## Related Documentation

* [Resource UI Control](../properties.json/ui-controls/resource.md)
* [Working with Resources](../hooks.js/working-with-resources.md)
* [rw.resizeResource()](../hooks.js/available-functions/rw.resizeresource.md)
* [@each](each.md)
* [Responsive Images & Media](../../guides/responsive-images-and-media.md)
* [Galleries & Resource Collections](../../guides/galleries-and-resource-collections.md)
