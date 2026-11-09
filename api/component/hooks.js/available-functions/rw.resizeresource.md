# rw.resizeResource()

The `rw.resizeResource()` function resizes an image resource to a specified width, returning the path to the resized image. This is essential for creating responsive images and thumbnails.

## Syntax

```javascript
const resizedPath = rw.resizeResource(resource, width);
```

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `resource` | Object | An image resource object from `rw.props` |
| `width` | Number | Target width in pixels |

## Returns

A string path to the resized image.

## Basic Example

```javascript
const transformHook = (rw) => {
    const { image } = rw.props;
    
    // Create a thumbnail at 400px wide
    const thumbnail = rw.resizeResource(image, 400);
    
    rw.setProps({
        thumbnail
    });
};

exports.transformHook = transformHook;
```

## Common Patterns

### Multiple Sizes

```javascript
const transformHook = (rw) => {
    const { image } = rw.props;
    
    rw.setProps({
        thumbnail: rw.resizeResource(image, 200),
        medium: rw.resizeResource(image, 600),
        large: rw.resizeResource(image, 1200),
        original: image.image
    });
};

exports.transformHook = transformHook;
```

### Retina/HiDPI Support

Double the width for retina displays:

```javascript
const transformHook = (rw) => {
    const { image } = rw.props;
    const displayWidth = 400;
    
    rw.setProps({
        // 2x for retina displays
        imageSrc: rw.resizeResource(image, displayWidth * 2),
        imageWidth: displayWidth
    });
};

exports.transformHook = transformHook;
```

### Responsive Images with Breakpoints

```javascript
const transformHook = (rw) => {
    const { image } = rw.props;
    const { breakpoints } = rw.theme;
    const { names, screens } = breakpoints;
    
    // Generate sources for each breakpoint
    const sources = names
        .filter(name => screens[name])
        .sort((a, b) => screens[b] - screens[a])
        .map(name => ({
            media: `(min-width: ${screens[name]}px)`,
            srcset: rw.resizeResource(image, screens[name] * 2),
            breakpoint: name
        }));
    
    rw.setProps({
        sources,
        fallbackSrc: rw.resizeResource(image, 800)
    });
};

exports.transformHook = transformHook;
```

### Gallery Thumbnails

```javascript
const transformHook = (rw) => {
    const { resources } = rw.props;
    
    // Process each image in a gallery
    if (resources?.resources) {
        resources.resources.forEach(resource => {
            resource.thumbnail = rw.resizeResource(resource, 400);
            resource.fullsize = resource.image;
        });
    }
    
    rw.setProps({
        images: resources?.resources || []
    });
};

exports.transformHook = transformHook;
```

### Responsive Image with Custom Sizes

```javascript
const transformHook = (rw) => {
    const { image } = rw.props;
    const { imageFileSize } = rw.responsiveProps;
    const { breakpoints } = rw.theme;
    const { names, screens } = breakpoints;
    
    // Use responsive prop values for sizes
    const sources = names
        .filter(name => imageFileSize[name] && screens[name])
        .sort((a, b) => screens[b] - screens[a])
        .map(name => ({
            media: `(min-width: ${screens[name]}px)`,
            srcset: rw.resizeResource(image, imageFileSize[name] * 2)
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

## Template Usage

```html
<!-- Simple resized image -->
<img src="{{thumbnail}}" alt="{{alt}}">

<!-- Responsive picture element -->
<picture>
    @each(source in sources)
        <source media="{{source.media}}" srcset="{{source.srcset}}">
    @endeach
    <img src="{{fallbackSrc}}" alt="{{alt}}">
</picture>
```

## Notes

- Always multiply width by 2 for retina display support
- The function returns a path string, not the full image object
- Works with any image resource from properties or collections
- Efficiently caches resized images
