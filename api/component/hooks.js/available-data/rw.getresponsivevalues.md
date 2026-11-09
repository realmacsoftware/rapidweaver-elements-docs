# rw.responsiveProps

The `rw.responsiveProps` object contains property values that vary by breakpoint. When a property is marked as responsive in `properties.json`, its per-breakpoint values are accessible here.

## Accessing Responsive Properties

```javascript
const transformHook = (rw) => {
    const { imageFileSize, columnCount } = rw.responsiveProps;
    
    // Each responsive property is an object with breakpoint keys
    console.log(imageFileSize);
    // { base: 400, sm: 600, md: 800, lg: 1200 }
    
    console.log(columnCount);
    // { base: 1, md: 2, lg: 3 }
};

exports.transformHook = transformHook;
```

## Structure

Responsive properties are objects keyed by breakpoint name:

```javascript
{
    base: value,    // Default/mobile value
    sm: value,      // Small screens
    md: value,      // Medium screens
    lg: value,      // Large screens
    xl: value,      // Extra large screens
    "2xl": value    // 2X large screens
}
```

Only breakpoints with explicitly set values are included.

## Example: Responsive Image Sizing

```javascript
const transformHook = (rw) => {
    const { breakpoints } = rw.theme;
    const { imageFileSize } = rw.responsiveProps;
    const { image } = rw.props;
    const { names, screens } = breakpoints;
    
    // Generate srcset for each breakpoint that has a size defined
    const sources = names
        .filter(name => imageFileSize[name] && screens[name])
        .sort((a, b) => screens[b] - screens[a])
        .map(name => ({
            media: `(min-width: ${screens[name]}px)`,
            srcset: rw.resizeResource(image, imageFileSize[name] * 2),
            breakpoint: name
        }));
    
    // Base/fallback size
    const fallbackSrc = rw.resizeResource(image, imageFileSize.base * 2);
    
    rw.setProps({
        sources,
        fallbackSrc
    });
};

exports.transformHook = transformHook;
```

## Example: Responsive Hidden States

```javascript
const transformHook = (rw) => {
    const { hidden } = rw.responsiveProps;
    
    // hidden = { base: true, md: false, lg: false }
    
    // Build visibility classes
    const visibilityClasses = Object.entries(hidden)
        .map(([breakpoint, isHidden]) => {
            const prefix = breakpoint === 'base' ? '' : `${breakpoint}:`;
            return isHidden ? `${prefix}hidden` : `${prefix}block`;
        })
        .join(' ');
    
    rw.setProps({
        visibilityClasses
    });
};

exports.transformHook = transformHook;
```

## Combining with Regular Props

Responsive props complement regular props - use `rw.props` for non-responsive values and `rw.responsiveProps` for breakpoint-specific values:

```javascript
const transformHook = (rw) => {
    // Non-responsive props
    const { image, alt, aspectRatio } = rw.props;
    
    // Responsive props
    const { imageWidth, padding } = rw.responsiveProps;
    
    rw.setProps({
        image,
        alt,
        aspectRatio,
        responsiveWidths: imageWidth,
        responsivePadding: padding
    });
};

exports.transformHook = transformHook;
```
