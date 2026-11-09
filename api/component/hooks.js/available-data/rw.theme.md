# rw.theme

The `rw.theme` object provides access to theme configuration, including responsive breakpoints.

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `breakpoints.names` | Array | Breakpoint names (e.g., `["sm", "md", "lg", "xl", "2xl"]`) |
| `breakpoints.screens` | Object | Breakpoint widths in pixels |

## Accessing Theme Data

```javascript
const transformHook = (rw) => {
    const { breakpoints } = rw.theme;
    const { names, screens } = breakpoints;

    console.log(names);   // ["sm", "md", "lg", "xl", "2xl"]
    console.log(screens); // { sm: 640, md: 768, lg: 1024, xl: 1280, "2xl": 1536 }
};

exports.transformHook = transformHook;
```

## Responsive Image Sources

A common use case is generating responsive image sources based on breakpoints:

```javascript
const transformHook = (rw) => {
    const { breakpoints } = rw.theme;
    const { names, screens } = breakpoints;
    const { image } = rw.props;

    // Generate responsive sources sorted by screen size (largest first)
    const sources = names
        .filter(name => screens[name])
        .sort((a, b) => screens[b] - screens[a])
        .map(name => ({
            media: `(min-width: ${screens[name]}px)`,
            srcset: rw.resizeResource(image, screens[name] * 2),
            breakpoint: name,
            minWidth: screens[name]
        }));

    rw.setProps({
        sources,
        fallbackSrc: image.image
    });
};

exports.transformHook = transformHook;
```

## Using Breakpoints for Conditional Logic

```javascript
const transformHook = (rw) => {
    const { breakpoints } = rw.theme;
    const { responsiveSettings } = rw.responsiveProps;

    // Access responsive property values at each breakpoint
    const { names } = breakpoints;

    names.forEach(breakpoint => {
        if (responsiveSettings[breakpoint]) {
            console.log(`Setting at ${breakpoint}:`, responsiveSettings[breakpoint]);
        }
    });
};

exports.transformHook = transformHook;
```

## Building Media Query Classes

```javascript
const transformHook = (rw) => {
    const { breakpoints } = rw.theme;
    const { hideOnMobile, hideOnDesktop } = rw.props;

    const visibilityClasses = [];

    if (hideOnMobile) {
        visibilityClasses.push('hidden', 'md:block');
    }

    if (hideOnDesktop) {
        visibilityClasses.push('block', 'lg:hidden');
    }

    rw.setProps({
        visibilityClasses: visibilityClasses.join(' ')
    });
};

exports.transformHook = transformHook;
```

## Using in Templates

```html
<!-- Generate picture element with responsive sources -->
<picture>
    @each(source in sources)
        <source media="{{source.media}}" srcset="{{source.srcset}}">
    @endeach
    <img src="{{fallbackSrc}}" alt="{{alt}}">
</picture>
```
