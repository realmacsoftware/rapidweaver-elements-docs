---
icon: anchor
---

# Hooks.js

Hooks provide a powerful way to extend your components by manipulating properties before they are applied within templates.

## Component Lifecycle

The typical flow of a component follows this sequence:

```
properties.json → hooks.js → template.html
```

1. **Properties** define the UI controls and their values
2. **Hooks** process and transform those values
3. **Templates** render the final HTML output

## Creating a Transform Hook

To use a transform hook, create a `hooks.js` file in the root of your component:

```javascript
const transformHook = (rw) => {
    // Access properties from UI controls
    const { title, isVisible } = rw.props;
    
    // Transform and pass data to templates
    rw.setProps({
        message: `Hello, ${title}!`,
        displayClass: isVisible ? 'block' : 'hidden'
    });
};

exports.transformHook = transformHook;
```

{% hint style="info" %}
Each component has its own unique `hooks.js` file. To share code across multiple components, we recommend using a build system or creating a script to merge and copy JS files to each component.
{% endhint %}

## The `rw` Object

The `rw` object is passed to your transform hook and provides access to component data and helper functions.

### Available Data

| Property | Description |
|----------|-------------|
| [`rw.props`](available-data/rw.props.md) | UI control values from properties.json |
| [`rw.responsiveProps`](available-data/rw.getresponsivevalues.md) | Responsive property values by breakpoint |
| [`rw.collections`](available-data/rw.collections.md) | Component collections data |
| [`rw.project`](available-data/rw.project.md) | Project-level data (title, mode, siteUrl, etc.) |
| [`rw.system`](available-data/rw.system.md) | Elements app version and build (not the component) |
| [`rw.page`](available-data/rw.page.md) | Current page data (id, title, filename, etc.) |
| [`rw.node`](available-data/rw.node.md) | Component node data (id, title, parent, etc.) |
| [`rw.component`](available-data/rw.element.md) | Component metadata (title, assetPath, etc.) |
| [`rw.theme`](available-data/rw.theme.md) | Theme data including breakpoints |
| [`rw.pages`](available-data/rw.pages.md) | Site navigation page tree |

### Available Functions

| Function | Description |
|----------|-------------|
| [`rw.setProps()`](available-functions/rw.setprops.md) | Pass data to templates |
| [`rw.setRootElement()`](available-functions/rw.setrootelement.md) | Configure the root HTML element |
| [`rw.addAnchor()`](available-functions/rw.addanchor.md) | Register an anchor for the link picker |
| [`rw.resizeResource()`](available-functions/rw.resizeresource.md) | Resize image resources |
| [`rw.getBreakpoints()`](available-functions/rw.getbreakpoints.md) | Get theme breakpoint data |

## Basic Example

Here's a complete example showing how hooks transform properties before they reach the template:

**properties.json**
```json
{
    "title": "Padding",
    "property": "padding",
    "default": 5,
    "slider": {
        "min": 0,
        "max": 12,
        "round": true
    }
}
```

**hooks.js**
```javascript
const transformHook = (rw) => {
    const { padding } = rw.props;
    
    // Double the padding value
    rw.setProps({
        padding: padding * 2
    });
};

exports.transformHook = transformHook;
```

**template.html**
```html
<div style="padding: {{padding}}px">
    Content with transformed padding
</div>
```

When the slider is set to 5, the template receives 10 (5 × 2).

## Conditional Class Generation

A common use case is generating CSS classes based on multiple properties:

```javascript
const transformHook = (rw) => {
    const {
        customSizing,
        size,
        fontSize,
        paddingTop,
        paddingRight,
        paddingBottom,
        paddingLeft
    } = rw.props;
    
    const sizeClasses = [
        !customSizing && size,
        customSizing && fontSize,
        customSizing && paddingTop,
        customSizing && paddingRight,
        customSizing && paddingBottom,
        customSizing && paddingLeft,
    ]
        .filter(Boolean)
        .join(" ");

    rw.setProps({
        classes: sizeClasses
    });
};

exports.transformHook = transformHook;
```

```html
<div class="{{classes}}">Content</div>
```

## Edit vs Preview Mode

You can detect whether the component is being viewed in the editor or preview:

```javascript
const transformHook = (rw) => {
    const { mode } = rw.project;
    
    rw.setProps({
        isEditMode: mode === 'edit',
        isPreviewMode: mode === 'preview'
    });
};

exports.transformHook = transformHook;
```

## Next Steps

- [Passing Data to Templates](passing-data-to-templates.md) - Detailed examples of using `rw.setProps()`
- [Working with Collections](working-with-collections.md) - Accessing and transforming collection data
- [Working with Resources](working-with-resources.md) - Handling images and other resources
- [Common Use Cases](common-use-cases.md) - Practical recipes and patterns
- [Building Complex Components](../../guides/README.md) - Guides showing hooks at work in real components
