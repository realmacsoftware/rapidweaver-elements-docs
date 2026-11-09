# rw.setRootElement()

The `rw.setRootElement()` function configures the root HTML element that wraps your component. This allows you to control the element tag, CSS classes, and HTML attributes.

## Syntax

```javascript
rw.setRootElement({
    as: 'tagName',      // HTML tag to use
    class: 'classes',   // CSS classes
    args: { }           // HTML attributes
});
```

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `as` | String | HTML tag name (e.g., `'div'`, `'section'`, `'article'`, `'a'`) |
| `class` | String | CSS classes to apply to the element |
| `args` | Object | HTML attributes as key-value pairs |

## Basic Examples

### Setting the Tag

```javascript
const transformHook = (rw) => {
    rw.setRootElement({
        as: 'section'
    });
};

exports.transformHook = transformHook;
```

Output: `<section>...</section>`

### Adding Classes

```javascript
const transformHook = (rw) => {
    const { padding, margin } = rw.props;
    
    rw.setRootElement({
        as: 'div',
        class: `container ${padding} ${margin}`
    });
};

exports.transformHook = transformHook;
```

Output: `<div class="container p-4 m-2">...</div>`

### Adding Attributes

```javascript
const transformHook = (rw) => {
    const { customId } = rw.props;
    
    rw.setRootElement({
        as: 'div',
        class: 'my-component',
        args: {
            id: customId,
            'data-theme': 'dark',
            'aria-label': 'Main content'
        }
    });
};

exports.transformHook = transformHook;
```

Output: `<div class="my-component" id="hero" data-theme="dark" aria-label="Main content">...</div>`

## Common Patterns

### Dynamic Tag Based on Link

```javascript
const transformHook = (rw) => {
    const { link } = rw.props;
    const hasLink = link && link.href && link.href.length > 0;
    
    rw.setRootElement({
        as: hasLink ? 'a' : 'div',
        class: 'card',
        args: hasLink ? {
            href: link.href,
            title: link.title,
            target: link.target
        } : {}
    });
    
    rw.setProps({ hasLink });
};

exports.transformHook = transformHook;
```

### Custom HTML Tag from Properties

```javascript
const transformHook = (rw) => {
    const { htmlTag, customTag } = rw.props;
    
    // Allow user to select tag or enter custom
    const tag = htmlTag === 'custom' 
        ? customTag.replace(/[^a-zA-Z0-9]/g, '') 
        : htmlTag;
    
    rw.setRootElement({
        as: tag || 'div'
    });
};

exports.transformHook = transformHook;
```

### Container with Full Styling

```javascript
const transformHook = (rw) => {
    const { 
        customId, 
        padding, 
        background, 
        shadow, 
        rounded 
    } = rw.props;
    const { id } = rw.node;
    
    const classes = [
        `group/${id}`,
        padding,
        background,
        shadow,
        rounded
    ].filter(Boolean).join(' ');
    
    rw.setRootElement({
        as: 'section',
        class: classes,
        args: {
            id: customId || undefined,
            'data-component': 'container'
        }
    });
    
    // Register anchor if custom ID is set
    if (customId) {
        rw.addAnchor(customId);
    }
};

exports.transformHook = transformHook;
```

### Alpine.js Integration

```javascript
const transformHook = (rw) => {
    const { id } = rw.node;
    
    rw.setRootElement({
        as: 'div',
        class: 'gallery',
        args: {
            'x-data': `gallery('${id}')`,
            'x-init': 'init()'
        }
    });
};

exports.transformHook = transformHook;
```

### Accordion/Disclosure Pattern

```javascript
const transformHook = (rw) => {
    const { id } = rw.node;
    const { openOnLoad } = rw.props;
    
    rw.setRootElement({
        as: 'div',
        class: `group/${id}`,
        args: {
            'x-data': `accordion('${id}', { openOnLoad: ${openOnLoad} })`,
            'x-bind': 'details',
            'data-open': 'false',
            'role': 'group',
            'aria-roledescription': 'accordion'
        }
    });
};

exports.transformHook = transformHook;
```

## Notes

- The `args` object is spread directly as HTML attributes
- Use `undefined` values to conditionally omit attributes
- Classes are concatenated into a single `class` attribute
- Works seamlessly with Tailwind CSS utility classes
