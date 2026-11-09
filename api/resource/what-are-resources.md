---
description: Project-managed files — images, video, audio, folders and more — and the four routes components use to consume them
icon: circle-question
---

# What are Resources?

Resources are the files a user adds to their Elements project — images, video, audio, entire folders of media, or any other file a site might need. Elements manages them in the project's Resources browser and takes care of storage and publishing. Your component never touches the file system: it declares that it wants a resource, and Elements hands it an object describing the file the user picked.

A resource can be:

* **An image** — the most common case, complete with intrinsic dimensions and alt text
* **Video or audio** — referenced by file path
* **A folder** — a whole set of resources treated as a single value, ideal for galleries and slideshows
* **Any other file** — SVGs, PDFs, documents, whatever your component can make use of

Resources can also be shipped inside an Element Pack itself, so a pack can provide ready-made assets alongside its [components](../component/components.md) and [templates](../template/what-are-templates.md) — see [What is an Element Pack?](../element-pack/what-is-an-element-pack.md)

## How Components Consume Resources

There are four routes a resource can take into your component.

### 1. The Resource UI Control

Declare a [`resource` control](../component/properties.json/ui-controls/resource.md) in your `properties.json` and Elements renders a dropwell in the inspector. The control accepts every file type by default; restrict it with the `accepts` and `excludes` options, which use the same token grammar as HTML's `<input accept>` attribute (`".svg"`, `"image/*"`, `"video/mp4"`). Whatever the user assigns becomes available to your templates and hooks under the control's `id`.

### 2. Resource Fields in Collection Items

[Collections](../component/collections/README.md) give users repeatable items — tabs, tracks, team members — and each item can carry its own resources. Add a `resource` control to the collection's `properties.json` and every item gets its own dropwell. The core Audio Playlist does exactly this: each track stores an artwork image and an audio file, which its template reads as `{{ track.coverImage }}` and `{{ track.audioSource.path }}`. See [Accessing Data in Templates](../component/collections/accessing-data-in-templates.md) for the template side.

### 3. Drag-and-Drop Targets

Add the `rwResourceDropZone` attribute to any element in your template — or to your root element from hooks — with a value matching a resource control's `id`. Users can then drag a file from Finder or the Resources browser straight onto your component on the canvas, and it lands in that property. The [Resource control reference](../component/properties.json/ui-controls/resource.md#resource-dropzones) covers the details, and any `accepts`/`excludes` restrictions filter which drops the target will take.

### 4. Processing Resources in Hooks

Resource objects arrive in `rw.props` like any other property, so your `hooks.js` can inspect and transform them before the template renders. The most common job is generating resized variants with [`rw.resizeResource()`](../component/hooks.js/available-functions/rw.resizeresource.md) — thumbnails, retina versions, per-breakpoint sources — and passing the results to the template with `rw.setProps()`. [Working with Resources](../component/hooks.js/working-with-resources.md) walks through the patterns.

## Resources in Practice: the Core Gallery

The open-source Gallery component (`com.realmacsoftware.gallery`) uses all of these routes at once. Its inspector declares a single resource control — `{"title": "Resources", "id": "resources", "resource": {}}` — that users fill with a folder of images, its empty state is a `rwResourceDropZone` drop target, and its hooks process every item in the folder before the template loops over them:

```javascript
// com.realmacsoftware.gallery/hooks.source.js
const transformHook = (rw) => {
    const { globalID, resources /* … */ } = rw.props;

    const hasResources = resources?.resources?.length > 0;

    resources?.resources?.forEach((resource) => {
        resource.thumbnail = rw.resizeResource(resource, 400);
        resource.alt = resource.alt || resource.caption || resource.author || "";
        // … video detection trimmed
    });

    // … class generation trimmed

    rw.setProps({
        hasResources,
        resources: resources?.resources,
        // … presentation props trimmed
    });
};

exports.transformHook = transformHook;
```

One folder resource in, a fully processed array out — each image gains a 400px thumbnail and a sensible alt fallback before the template ever sees it.

## Learn More

{% content-ref url="../component/hooks.js/working-with-resources.md" %}
[Working with Resources — the hooks-side patterns for images, folders, and placeholders](../component/hooks.js/working-with-resources.md)
{% endcontent-ref %}

{% content-ref url="../guides/galleries-and-resource-collections.md" %}
[Galleries & Resource Collections — a guided tour of the core Gallery component](../guides/galleries-and-resource-collections.md)
{% endcontent-ref %}

## Related Documentation

* [Resource UI Control](../component/properties.json/ui-controls/resource.md)
* [rw.resizeResource()](../component/hooks.js/available-functions/rw.resizeresource.md)
* [Working with Resources](../component/hooks.js/working-with-resources.md)
* [Collections](../component/collections/README.md)
* [What is an Element Pack?](../element-pack/what-is-an-element-pack.md)
