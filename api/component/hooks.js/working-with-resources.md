# Working with Resources

Resources in Elements are typically images or files that users add to components. This guide covers how to work with image resources in hooks.

## Resource Object Structure

When a user adds an image via a resource control, the resource object contains:

```javascript
{
    image: "/path/to/image.jpg",  // Path to the image file
    width: 1920,                   // Original width in pixels
    height: 1080,                  // Original height in pixels
    aspect: "16/9",               // Aspect ratio string
    alt: "Image description",      // Alt text
    format: "jpg"                  // File format
}
```

## Accessing Resources

```javascript
const transformHook = (rw) => {
    const { image, backgroundImage } = rw.props;
    
    // Check if resource exists and has an image
    const hasImage = image && image.image;
    
    if (hasImage) {
        console.log(image.image);  // "/resources/my-image.jpg"
        console.log(image.width);  // 1920
        console.log(image.height); // 1080
    }
    
    rw.setProps({
        hasImage,
        imageSrc: hasImage ? image.image : null,
        imageAlt: hasImage ? image.alt : ''
    });
};

exports.transformHook = transformHook;
```

## Resizing Images

Use `rw.resizeResource()` to create optimized versions of images:

```javascript
const transformHook = (rw) => {
    const { image } = rw.props;
    
    if (!image || !image.image) {
        rw.setProps({ hasImage: false });
        return;
    }
    
    rw.setProps({
        hasImage: true,
        // Create different sizes
        thumbnail: rw.resizeResource(image, 200),
        small: rw.resizeResource(image, 400),
        medium: rw.resizeResource(image, 800),
        large: rw.resizeResource(image, 1200),
        // Keep original for full-size viewing
        original: image.image
    });
};

exports.transformHook = transformHook;
```

## Retina/HiDPI Support

Always double the intended display width for retina displays:

```javascript
const transformHook = (rw) => {
    const { image } = rw.props;
    const displayWidth = 400; // CSS width
    
    rw.setProps({
        // 2x for retina displays
        imageSrc: rw.resizeResource(image, displayWidth * 2),
        imageWidth: displayWidth
    });
};

exports.transformHook = transformHook;
```

## Responsive Images

Generate sources for a `<picture>` element:

```javascript
const transformHook = (rw) => {
    const { image } = rw.props;
    const { breakpoints } = rw.theme;
    const { names, screens } = breakpoints;
    
    if (!image?.image) {
        rw.setProps({ hasImage: false });
        return;
    }
    
    // Generate sources for each breakpoint
    const sources = names
        .filter(name => screens[name])
        .sort((a, b) => screens[b] - screens[a])
        .map(name => ({
            media: `(min-width: ${screens[name]}px)`,
            srcset: rw.resizeResource(image, screens[name] * 2)
        }));
    
    rw.setProps({
        hasImage: true,
        sources,
        fallbackSrc: rw.resizeResource(image, 800),
        alt: image.alt || '',
        aspectRatio: image.aspect
    });
};

exports.transformHook = transformHook;
```

Template:

```html
@if(hasImage)
<picture>
    @each(source in sources)
        <source media="{{source.media}}" srcset="{{source.srcset}}">
    @endeach
    <img 
        src="{{fallbackSrc}}" 
        alt="{{alt}}"
        style="aspect-ratio: {{aspectRatio}}"
    >
</picture>
@endif
```

## Gallery Resources

Process multiple images from a resource gallery:

```javascript
const transformHook = (rw) => {
    const { resources } = rw.props;
    
    if (!resources?.resources?.length) {
        rw.setProps({ 
            hasImages: false,
            images: [] 
        });
        return;
    }
    
    // Process each image
    const images = resources.resources.map(resource => ({
        ...resource,
        thumbnail: rw.resizeResource(resource, 400),
        fullsize: resource.image,
        alt: resource.caption || resource.author || '',
        isVideo: ['youtube', 'vimeo', 'mp4'].includes(resource.format)
    }));
    
    rw.setProps({
        hasImages: true,
        images,
        imageCount: images.length
    });
};

exports.transformHook = transformHook;
```

## Placeholder Images

Show placeholders in edit mode when no image is set:

```javascript
const transformHook = (rw) => {
    const { image } = rw.props;
    const { mode } = rw.project;
    const { sharedAssetPath } = rw.component;
    
    const hasImage = image && image.image;
    const isEditMode = mode === 'edit';
    
    // Use placeholder in edit mode when no image is set
    const displayImage = hasImage 
        ? image.image 
        : (isEditMode ? `${sharedAssetPath}/images/placeholder.png` : null);
    
    rw.setProps({
        hasImage,
        displayImage,
        showPlaceholder: isEditMode && !hasImage
    });
};

exports.transformHook = transformHook;
```

## Background Images

Generate CSS background image classes:

```javascript
const transformHook = (rw) => {
    const { backgroundImage } = rw.props;
    
    if (!backgroundImage?.image) {
        rw.setProps({ hasBackground: false });
        return;
    }
    
    const bgClasses = [
        `bg-[url(${backgroundImage.image})]`,
        'bg-cover',
        'bg-center',
        'bg-no-repeat'
    ].join(' ');
    
    rw.setProps({
        hasBackground: true,
        bgClasses
    });
};

exports.transformHook = transformHook;
```
