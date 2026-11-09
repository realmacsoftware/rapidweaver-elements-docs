# Common Use Cases

Practical recipes and patterns for working with hooks.js, based on real-world components.

## Conditional Class Generation

Build CSS class strings based on multiple properties:

```javascript
const transformHook = (rw) => {
    const {
        size,
        variant,
        isRounded,
        hasShadow,
        customClasses
    } = rw.props;
    
    const classes = [
        // Size classes
        size,
        
        // Variant styles
        variant === 'primary' && 'bg-blue-500 text-white',
        variant === 'secondary' && 'bg-gray-200 text-gray-800',
        
        // Optional modifiers
        isRounded && 'rounded-lg',
        hasShadow && 'shadow-md',
        
        // User's custom classes
        customClasses
    ]
        .filter(Boolean)
        .join(' ');
    
    rw.setProps({ classes });
};

exports.transformHook = transformHook;
```

## Edit vs Preview Mode Branching

Show different content or behavior based on the current mode:

```javascript
const transformHook = (rw) => {
    const { mode } = rw.project;
    const { sharedAssetPath } = rw.component;
    const { image, video } = rw.props;
    
    const isEditMode = mode === 'edit';
    const hasImage = image && image.image;
    
    // Show placeholder in edit mode when no image is set
    const displayImage = hasImage 
        ? image.image 
        : (isEditMode ? `${sharedAssetPath}/images/placeholder.png` : null);
    
    // Don't autoplay videos in edit mode
    const videoAutoplay = !isEditMode;
    
    // Include interactive features only in preview
    const includeInteractive = !isEditMode;
    
    rw.setProps({
        isEditMode,
        displayImage,
        hasImage,
        videoAutoplay,
        includeInteractive
    });
};

exports.transformHook = transformHook;
```

## Responsive Image Handling

Generate responsive image sources based on theme breakpoints:

```javascript
const transformHook = (rw) => {
    const { image } = rw.props;
    const { breakpoints } = rw.theme;
    const { names, screens } = breakpoints;
    
    if (!image || !image.image) {
        rw.setProps({ hasImage: false });
        return;
    }
    
    // Generate sources for each breakpoint, largest first
    const sources = names
        .filter(name => screens[name])
        .sort((a, b) => screens[b] - screens[a])
        .map(name => ({
            media: `(min-width: ${screens[name]}px)`,
            srcset: rw.resizeResource(image, screens[name] * 2), // 2x for retina
            breakpoint: name
        }));
    
    rw.setProps({
        hasImage: true,
        sources,
        fallbackSrc: rw.resizeResource(image, 800),
        alt: image.alt || ''
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
    <img src="{{fallbackSrc}}" alt="{{alt}}">
</picture>
@endif
```

## Root Element Configuration

Configure the wrapper element with dynamic tag, classes, and attributes:

```javascript
const transformHook = (rw) => {
    const { 
        customId,
        link,
        padding,
        background,
        shadow,
        htmlTag
    } = rw.props;
    const { id } = rw.node;
    
    // Determine if this should be a link
    const hasLink = link && link.href && link.href.length > 0;
    
    // Build class list
    const wrapperClasses = [
        `group/${id}`,
        padding,
        background,
        shadow
    ].filter(Boolean).join(' ');
    
    // Configure root element
    rw.setRootElement({
        as: hasLink ? 'a' : (htmlTag || 'div'),
        class: wrapperClasses,
        args: {
            id: customId || undefined,
            ...(hasLink ? {
                href: link.href,
                title: link.title,
                target: link.target
            } : {})
        }
    });
    
    // Register anchor if custom ID is set
    if (customId && customId.length > 0) {
        rw.addAnchor(customId);
    }
    
    rw.setProps({ hasLink });
};

exports.transformHook = transformHook;
```

## Collection Data Transformation

Process and enhance collection data:

```javascript
const transformHook = (rw) => {
    const { items } = rw.collections;
    
    if (!items || items.length === 0) {
        rw.setProps({ 
            hasItems: false,
            items: [] 
        });
        return;
    }
    
    // Enhance each item with computed properties
    const enhancedItems = items.map((item, index) => ({
        ...item,
        isFirst: index === 0,
        isLast: index === items.length - 1,
        index: index,
        // Generate thumbnail if item has an image
        thumbnail: item.image ? rw.resizeResource(item.image, 400) : null
    }));
    
    // Calculate aggregate data
    const totalPrice = items
        .filter(item => item.price)
        .reduce((sum, item) => sum + item.price, 0);
    
    rw.setProps({
        hasItems: true,
        items: enhancedItems,
        itemCount: items.length,
        totalPrice,
        formattedTotal: `$${totalPrice.toFixed(2)}`
    });
};

exports.transformHook = transformHook;
```

## Filter Tags for Filtering

Set up data attributes for JavaScript-based filtering:

```javascript
const transformHook = (rw) => {
    const { tags } = rw.collections;
    const { filterGroup, customGroupId } = rw.props;
    const { parent } = rw.node;
    
    // Create comma-separated tag list for data attribute
    const dataTags = tags 
        ? tags.map(tag => tag.title).join(',') 
        : '';
    
    // Determine filter group ID
    const groupId = filterGroup === 'parent' 
        ? parent.id 
        : customGroupId;
    
    rw.setRootElement({
        as: 'div',
        class: 'filter-item',
        args: {
            'data-filter-tags': dataTags,
            'data-filter-group': groupId
        }
    });
    
    rw.setProps({
        tags,
        hasTags: tags && tags.length > 0
    });
};

exports.transformHook = transformHook;
```

## Alpine.js Integration

Set up Alpine.js data and bindings via `rw.setRootElement()`. Pass structured config through a `data-*` attribute — do not interpolate JSON into the `x-data` expression (the JSON's double-quotes break the HTML attribute parse).

```javascript
const transformHook = (rw) => {
    const { id } = rw.node;
    const { openOnLoad, animation } = rw.props;
    
    // Configure for accordion behavior
    const config = {
        openOnLoad: openOnLoad === 'true',
        animation: animation
    };
    
    rw.setRootElement({
        as: 'div',
        class: `group/${id}`,
        args: {
            'x-data': `accordion('${id}')`,
            'data-config': JSON.stringify(config),
            'x-bind': 'details',
            'data-open': 'false',
            'role': 'group',
            'aria-roledescription': 'accordion'
        }
    });
    
    rw.setProps({
        nodeId: id,
        showContent: rw.project.mode !== 'edit' || openOnLoad === 'true'
    });
};

exports.transformHook = transformHook;
```
