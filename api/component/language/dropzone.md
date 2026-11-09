---
description: Create areas where child elements can be added
---

# @dropzone

The `@dropzone` directive creates an area within a template where child elements can be added. Dropzones are fundamental to building container components that allow users to compose layouts by dragging and dropping other components inside them.

## Syntax

```html
@dropzone("name")
```

With additional parameters:

```html
@dropzone(name: "content", title: "Display Title", horizontal: true)
```

## Parameters

| Parameter    | Required | Description                                                              |
| ------------ | -------- | ------------------------------------------------------------------------ |
| `name`       | Yes      | A unique identifier for the dropzone within the component                |
| `title`      | No       | The label displayed in the editor interface                              |
| `horizontal` | No       | When `true`, displays dropped items in a horizontal layout in the editor |

## Examples

### Basic Dropzone

```html
@dropzone("content")
```

### Named Dropzone with Title

Provide a descriptive title for the editor interface:

```html
@dropzone("content", title: "Container")
```

### Horizontal Layout

Use horizontal layout for grid or flex containers:

```html
@dropzone(name: "content", title: "Grid", horizontal: true)
```

### Multiple Dropzones in One Component

Components can have multiple named dropzones for different content areas:

```html
<div class="accordion-header">
    @dropzone("title", title: "Title")
</div>
<div class="accordion-content">
    @dropzone("content", title: "Content")
</div>
```

### Navbar with Multiple Dropzones

A navigation component with separate areas for logo, menu items, and mobile content:

```html
<nav class="navbar">
    <div class="logo-area">
        @dropzone("logo", title: "Logo")
    </div>
    <div class="desktop-items">
        @dropzone("desktop", title: "Desktop")
    </div>
</nav>

@portal("bodyStart")
    <div class="mobile-menu">
        @dropzone("mobileLogo", title: "Mobile Logo")
        @dropzone("mobileContent", title: "Mobile Content")
    </div>
@endportal
```

### Modal with Trigger and Content

```html
<span class="trigger">
    @dropzone("trigger", title: "Trigger")
</span>

@portal("bodyEnd")
    <div class="modal-panel">
        @dropzone("content", title: "Content")
    </div>
@endportal
```

### Flex Container with Direction Option

```html
@if(wantsHorizontalDropzone)
    @dropzone(name: "content", title: "Flex", horizontal: true)
@else
    @dropzone(name: "content", title: "Flex")
@endif
```

## Dropzones Inside Loops

Dropzones can be placed inside `@each` loops to create dynamic, repeating content areas. This is useful for components like tab panels, accordion sections, or multi-column layouts where each iteration needs its own dropzone.

The dropzone name and title must be static text—you cannot use dynamic values like `{{index}}` or template variables inside the dropzone declaration. Elements automatically handles creating unique dropzones for each loop iteration.

### Basic Loop Dropzone

Place a dropzone inside a loop with a static name:

```html
@each(tab in tabs)
    <div class="tab-panel">
        @dropzone("panel", title: "Panel")
    </div>
@endeach
```

### Accordion with Dynamic Panels

Create an accordion where each panel has its own content dropzone:

```html
@each(section in sections)
    <div class="accordion-item">
        <button class="accordion-header">
            {{section.title}}
        </button>
        <div class="accordion-body">
            @dropzone("content", title: "Section Content")
        </div>
    </div>
@endeach
```

## Resource Dropzones

In addition to component dropzones, you can allow users to drop resources (like images) directly into the editor using the `rwResourceDropZone` HTML attribute.

### Syntax

```html
<div rwResourceDropZone="propertyName">
    <!-- Fallback content -->
</div>
```

### Image Gallery Example

Allow users to drop a folder of images directly into the component:

```html
<div class="gallery" rwResourceDropZone="images">
    @if(!images.isFolder)
        <h3 class="placeholder">
            Drop a folder of images here!
        </h3>
    @else
        @each(image in images.resources)
            <img src="{{image.image}}" alt="{{image.caption}}" />
        @endeach
    @endif
</div>
```

This requires a corresponding resource control in the Properties file:

```json
{
    "groups": [{
        "title": "Content",
        "properties": [{
            "title": "Images",
            "property": "images",
            "resource": {}
        }]
    }]
}
```

## Best Practices

1. **Use descriptive names** - Choose names that clearly indicate the purpose of the dropzone (e.g., `"header"`, `"content"`, `"sidebar"`).
2. **Add meaningful titles** - The `title` parameter helps users understand where to add content in the editor.
3. **Use `horizontal` for layout components** - Enable horizontal layout for flex/grid containers to match the visual layout in the editor.
4. **Avoid duplicate visible dropzones** - While multiple dropzones can share a name, only show one at a time to prevent confusion.
5. **Combine with @portal for overlays** - For modals and off-canvas menus, use `@portal` to position the dropzone content appropriately in the DOM.

## Related Documentation

* [Collection-Driven Dropzones](../../guides/collection-driven-dropzones.md) - Generating a dropzone per collection item
* [Modals, Overlays & Portals](../../guides/modals-overlays-and-portals.md) - Dropzones inside portal-teleported panels
