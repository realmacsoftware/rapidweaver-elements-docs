# Available Functions

The `rw` object provides several functions for manipulating component output and behavior.

## Quick Reference

| Function | Description |
|----------|-------------|
| [`rw.setProps()`](rw.setprops.md) | Pass data to templates |
| [`rw.setRootElement()`](rw.setrootelement.md) | Configure the root HTML element |
| [`rw.addAnchor()`](rw.addanchor.md) | Register an anchor for the link picker |
| [`rw.resizeResource()`](rw.resizeresource.md) | Resize image resources |
| [`rw.getBreakpoints()`](rw.getbreakpoints.md) | Get theme breakpoint configuration |

## Basic Usage

```javascript
const transformHook = (rw) => {
    const { title, customId, image } = rw.props;
    
    // Pass data to templates
    rw.setProps({
        title,
        displayTitle: title.toUpperCase()
    });
    
    // Configure the root HTML element
    rw.setRootElement({
        as: 'section',
        class: 'my-component p-4',
        args: { id: customId }
    });
    
    // Register anchor for link picker
    if (customId) {
        rw.addAnchor(customId);
    }
    
    // Resize image for thumbnail
    const thumbnail = rw.resizeResource(image, 400);
};

exports.transformHook = transformHook;
```

## Function Details

### setProps

The primary way to pass data to your templates. Any data passed here becomes available in template files.

```javascript
rw.setProps({
    message: "Hello",
    items: [1, 2, 3],
    config: { enabled: true }
});
```

### setRootElement

Configure the wrapper element that Elements generates for your component. Control the tag name, CSS classes, and HTML attributes.

```javascript
rw.setRootElement({
    as: 'article',
    class: 'card shadow-lg',
    args: { 
        id: 'my-card',
        'data-theme': 'dark'
    }
});
```

### addAnchor

Register a custom anchor ID so users can link directly to this component instance using the link picker.

```javascript
rw.addAnchor('contact-form');
```

### resizeResource

Resize an image resource to a specific width. Returns the path to the resized image.

```javascript
const thumbnailPath = rw.resizeResource(imageResource, 300);
```
