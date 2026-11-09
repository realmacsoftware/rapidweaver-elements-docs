---
description: Access data in your transform hook
---

# Available Data

The `rw` object passed to your transform hook provides access to various data sources. Most data needs to be passed to templates using `rw.setProps()`, except for `node` which is always available.

## Quick Reference

| Property | Description |
|----------|-------------|
| [`rw.props`](rw.props.md) | UI control values from properties.json |
| [`rw.responsiveProps`](rw.getresponsivevalues.md) | Responsive property values by breakpoint |
| [`rw.collections`](rw.collections.md) | Component collections data |
| [`rw.project`](rw.project.md) | Project-level settings |
| [`rw.system`](rw.system.md) | Elements app version and build |
| [`rw.page`](rw.page.md) | Current page information |
| [`rw.node`](rw.node.md) | Component instance data (always available in templates) |
| [`rw.component`](rw.element.md) | Component metadata and asset paths |
| [`rw.theme`](rw.theme.md) | Theme configuration including breakpoints |
| [`rw.pages`](rw.pages.md) | Site navigation page tree |

## Basic Example

```javascript
const transformHook = (rw) => {
    // Access various data sources
    const { title, isVisible } = rw.props;
    const { items } = rw.collections;
    const { mode } = rw.project;
    const { id } = rw.node;
    const { assetPath } = rw.component;
    
    // Pass to templates
    rw.setProps({
        title,
        isVisible,
        items,
        isEditMode: mode === 'edit',
        nodeId: id,
        iconPath: `${assetPath}/icons/`
    });
};

exports.transformHook = transformHook;
```

## Exposing Data to Templates

While the `node` object is automatically available, other data must be explicitly passed:

```javascript
const transformHook = (rw) => {    
    // Expose project, page and component objects to the template
    rw.setProps({
        project: rw.project,
        page: rw.page,
        component: rw.component
    });
};

exports.transformHook = transformHook;
```

With this in place, you can access properties in your templates:

```html
<!-- Project data -->
<title>{{project.title}}</title>

<!-- Page data -->
<h1>{{page.title}}</h1>
<p>Path: {{page.absolutePath}}</p>

<!-- Component data -->
<img src="{{component.assetPath}}/placeholder.png">

<!-- Node is always available -->
<div id="{{node.id}}">{{node.title}}</div>
```

## Data Availability by Mode

Some data may differ between edit and preview modes:

```javascript
const transformHook = (rw) => {
    const { mode } = rw.project;
    const { sharedAssetPath } = rw.component;
    const { image } = rw.props;
    
    // Show placeholder in edit mode when no image is set
    const displayImage = image?.image 
        ? image.image 
        : (mode === 'edit' ? `${sharedAssetPath}/images/placeholder.png` : null);
    
    rw.setProps({
        displayImage,
        hasImage: !!image?.image
    });
};

exports.transformHook = transformHook;
```
