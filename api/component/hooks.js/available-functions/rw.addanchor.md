# rw.addAnchor()

The `rw.addAnchor()` function registers a custom anchor ID for your component, making it available in the link picker's "Anchor" menu so users can link directly to this component.

## Syntax

```javascript
rw.addAnchor(anchorId);
```

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `anchorId` | String | The anchor ID to register (without the `#` symbol) |

## Basic Example

```javascript
const transformHook = (rw) => {
    const { customId } = rw.props;
    
    if (customId && customId.length > 0) {
        rw.addAnchor(customId);
    }
};

exports.transformHook = transformHook;
```

## Complete Pattern

When using anchors, you typically also need to set the `id` attribute on the root element:

```javascript
const transformHook = (rw) => {
    const { customId } = rw.props;
    
    // Set the ID on the root element
    rw.setRootElement({
        as: 'section',
        class: 'my-component',
        args: {
            id: customId || undefined
        }
    });
    
    // Register the anchor for the link picker
    if (customId && customId.length > 0) {
        rw.addAnchor(customId);
    }
};

exports.transformHook = transformHook;
```

## How It Works

1. User sets a custom ID in the component's properties (e.g., "contact-form")
2. Your hook calls `rw.addAnchor('contact-form')`
3. The anchor appears in the link picker's Anchor menu
4. When selected, it creates a link like `#contact-form`
5. Clicking the link scrolls to your component

## Example with Fallback

```javascript
const transformHook = (rw) => {
    const { customId } = rw.props;
    const { id } = rw.node;
    
    // Use custom ID if provided, otherwise use node ID
    const anchorId = customId || id;
    
    rw.setRootElement({
        as: 'div',
        args: { id: anchorId }
    });
    
    // Only register custom IDs (not auto-generated node IDs)
    if (customId && customId.length > 0) {
        rw.addAnchor(customId);
    }
};

exports.transformHook = transformHook;
```

## Notes

- Only call `addAnchor` when you have a valid, non-empty ID
- The anchor ID should match the `id` attribute on your root element
- Anchors are automatically available to other pages in the same project
- Users can link to anchors using the standard link picker interface
