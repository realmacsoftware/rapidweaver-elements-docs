# rw.setProps()

The `rw.setProps()` function passes data from your hook to your templates. Any data passed becomes available as template variables.

Values you set here go to your templates only — they won't show up back in `rw.props`. Rather than setting a value and reading it back later, keep your working values in local variables and pass the finished results to `rw.setProps()` at the end of your hook.

## Syntax

```javascript
rw.setProps({
    key: value,
    anotherKey: anotherValue
});
```

## Basic Examples

### Simple Values

```javascript
const transformHook = (rw) => {
    rw.setProps({
        message: 'Hello, World!',
        count: 42,
        isVisible: true
    });
};

exports.transformHook = transformHook;
```

In templates:

```html
<p>{{message}}</p>
<span>Count: {{count}}</span>
@if(isVisible)
    <div>Visible content</div>
@endif
```

### Arrays

```javascript
const transformHook = (rw) => {
    rw.setProps({
        team: ["Ben", "Dan", "Tom"],
        numbers: [1, 2, 3, 4, 5]
    });
};

exports.transformHook = transformHook;
```

In templates:

```html
<ul>
    @each(member in team)
        <li>{{member}}</li>
    @endeach
</ul>
```

### Objects

```javascript
const transformHook = (rw) => {
    rw.setProps({
        apps: {
            elements: {
                slogan: "Build beautiful websites. No code required.",
                isAmazing: true
            },
            squash: {
                slogan: "Batch Photo Editor",
                isAmazing: true
            }
        }
    });
};

exports.transformHook = transformHook;
```

In templates:

```html
<p>{{apps.elements.slogan}}</p>
@if(apps.elements.isAmazing)
    <span>Amazing!</span>
@endif
```

## Common Patterns

### Passing Transformed Props

```javascript
const transformHook = (rw) => {
    const { firstName, lastName, price, quantity } = rw.props;
    
    rw.setProps({
        fullName: `${firstName} ${lastName}`,
        total: price * quantity,
        formattedTotal: `$${(price * quantity).toFixed(2)}`
    });
};

exports.transformHook = transformHook;
```

### Conditional Values

```javascript
const transformHook = (rw) => {
    const { size, customSize } = rw.props;
    
    rw.setProps({
        displaySize: customSize || size,
        hasCustomSize: !!customSize
    });
};

exports.transformHook = transformHook;
```

### Spreading Collections

```javascript
const transformHook = (rw) => {
    // Pass all collections to templates
    rw.setProps({
        ...rw.collections
    });
};

exports.transformHook = transformHook;
```

### Building CSS Classes

```javascript
const transformHook = (rw) => {
    const { padding, margin, rounded, shadow } = rw.props;
    
    const classes = [
        padding,
        margin,
        rounded && 'rounded-lg',
        shadow && 'shadow-md'
    ].filter(Boolean).join(' ');
    
    rw.setProps({
        classes
    });
};

exports.transformHook = transformHook;
```

## Multiple Calls

You can call `setProps` multiple times. Properties are merged:

```javascript
const transformHook = (rw) => {
    rw.setProps({
        title: 'Hello'
    });
    
    // This adds to existing props, doesn't replace them
    rw.setProps({
        subtitle: 'World'
    });
    
    // Both title and subtitle are now available in templates
};

exports.transformHook = transformHook;
```

## Passing Context Objects

```javascript
const transformHook = (rw) => {
    rw.setProps({
        project: rw.project,
        page: rw.page,
        component: rw.component
    });
};

exports.transformHook = transformHook;
```
