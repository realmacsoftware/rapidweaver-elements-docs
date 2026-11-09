---
description: Process and manipulate collection data in the hooks file
---

# Data Collections in hooks.js

The hooks.js file gives you access to collection data through the `rw.collections` object. This allows you to process, transform, or validate collection data before it reaches your templates.

## Accessing Collections

Access collections via `rw.collections.{collection-name}`:

```javascript
const transformHook = (rw) => {
    const { features } = rw.collections;
    
    // features is an array of collection items
    console.log(features); // [{title: "...", description: "..."}, ...]
};

exports.transformHook = transformHook;
```

## Automatic Template Injection

All collections are automatically available in templates via the `collections` object. You don't need to pass them explicitly unless you've transformed the data:

```html
<!-- This works automatically -->
@each(feature in collections.features)
    <div>{{feature.title}}</div>
@endeach
```

## Common Patterns

### Checking for Empty Collections

Determine if a collection has items and pass a boolean to your template:

```javascript
const transformHook = (rw) => {
    const { features } = rw.collections;
    
    const hasFeatures = features && features.length > 0;
    
    rw.setProps({ hasFeatures });
};

exports.transformHook = transformHook;
```

**Template usage:**
```html
@if(hasFeatures)
    @each(feature in collections.features)
        <div>{{feature.title}}</div>
    @endeach
@else
    <p>No features added yet.</p>
@endif
```

### Getting the First Item

Extract the first item for special display (like a "now playing" track):

```javascript
const transformHook = (rw) => {
    const { tracks } = rw.collections;
    const { sharedAssetPath } = rw.component;
    
    // Get first track with fallback values
    const firstTrack = tracks?.[0] || {
        title: "Placeholder Title",
        artist: "Placeholder Artist",
        coverImage: `${sharedAssetPath}/images/placeholder.jpg`,
        audioSource: { path: "" }
    };
    
    const hasMultipleTracks = tracks?.length > 1;
    
    rw.setProps({
        tracks,
        firstTrack,
        hasMultipleTracks
    });
};

exports.transformHook = transformHook;
```

**Template usage:**
```html
<!-- Display first track prominently -->
<div class="now-playing">
    <img src="{{firstTrack.coverImage}}" alt="Cover" />
    <h3>{{firstTrack.title}}</h3>
    <p>{{firstTrack.artist}}</p>
</div>

<!-- List remaining tracks -->
@if(hasMultipleTracks)
    <ul class="playlist">
        @each(track in tracks)
            <li>{{track.title}}</li>
        @endeach
    </ul>
@endif
```

### Extracting Values for Data Attributes

Transform collection data into formats needed for JavaScript or data attributes:

```javascript
const transformHook = (rw) => {
    const { tags } = rw.collections;
    
    // Convert tags array to comma-separated string for filtering
    const filterTags = tags?.map((tag) => tag.title).join(",") || "";
    
    rw.setRootElement({
        as: "div",
        class: "filterable-item",
        args: {
            "data-filter-tags": filterTags
        }
    });
};

exports.transformHook = transformHook;
```

This outputs: `<div class="filterable-item" data-filter-tags="tag1,tag2,tag3">`

### Filtering Collection Items

Filter collection items based on conditions:

```javascript
const transformHook = (rw) => {
    const { items } = rw.collections;
    const { showFeaturedOnly } = rw.props;
    
    // Filter to featured items only if enabled
    const displayItems = showFeaturedOnly 
        ? items?.filter(item => item.featured) 
        : items;
    
    rw.setProps({ displayItems });
};

exports.transformHook = transformHook;
```

### Sorting Collection Items

Sort collection items by a property:

```javascript
const transformHook = (rw) => {
    const { items } = rw.collections;
    const { sortBy, sortOrder } = rw.props;
    
    const sortedItems = [...(items || [])].sort((a, b) => {
        const valueA = a[sortBy] || "";
        const valueB = b[sortBy] || "";
        
        if (sortOrder === "desc") {
            return valueB.localeCompare(valueA);
        }
        return valueA.localeCompare(valueB);
    });
    
    rw.setProps({ sortedItems });
};

exports.transformHook = transformHook;
```

### Adding Computed Properties

Enhance collection items with computed values:

```javascript
const transformHook = (rw) => {
    const { products } = rw.collections;
    
    // Add computed properties to each item
    const enhancedProducts = products?.map((product, index) => ({
        ...product,
        isOnSale: product.salePrice < product.regularPrice,
        savings: product.regularPrice - product.salePrice,
        displayOrder: index + 1
    })) || [];
    
    rw.setProps({ products: enhancedProducts });
};

exports.transformHook = transformHook;
```

### Grouping Items

Group collection items by a property:

```javascript
const transformHook = (rw) => {
    const { items } = rw.collections;
    
    // Group items by category
    const groupedItems = items?.reduce((groups, item) => {
        const category = item.category || "Uncategorized";
        if (!groups[category]) {
            groups[category] = [];
        }
        groups[category].push(item);
        return groups;
    }, {}) || {};
    
    // Convert to array for template iteration
    const categories = Object.entries(groupedItems).map(([name, items]) => ({
        name,
        items
    }));
    
    rw.setProps({ categories });
};

exports.transformHook = transformHook;
```

**Template usage:**
```html
@each(category in categories)
    <section>
        <h2>{{category.name}}</h2>
        @each(item in category.items)
            <div>{{item.title}}</div>
        @endeach
    </section>
@endeach
```

### Limiting Display Count

Limit the number of items displayed:

```javascript
const transformHook = (rw) => {
    const { testimonials } = rw.collections;
    const { maxDisplay } = rw.props;
    
    const displayTestimonials = testimonials?.slice(0, maxDisplay) || [];
    const hasMore = testimonials?.length > maxDisplay;
    
    rw.setProps({ 
        displayTestimonials,
        hasMore,
        totalCount: testimonials?.length || 0
    });
};

exports.transformHook = transformHook;
```

## Full Example: Audio Playlist

Here's how the Audio Playlist component processes its tracks collection:

```javascript
const transformHook = (rw) => {
    const { tracks } = rw.collections;
    const { sharedAssetPath } = rw.component;
    const { mode } = rw.project;
    
    // Get first track with placeholder fallback
    const firstTrack = tracks?.[0] || {
        title: "Placeholder Title",
        artist: "Placeholder Artist",
        coverImage: `${sharedAssetPath}/images/image-square.jpg`,
        audioSource: {
            path: "https://example.com/placeholder.mp3"
        }
    };
    
    const hasMultipleTracks = tracks?.length > 1;
    
    rw.setProps({
        id: rw.node.id,
        edit: mode === "edit",
        tracks,
        firstTrack,
        hasMultipleTracks
    });
};

exports.transformHook = transformHook;
```

## Best Practices

1. **Always handle empty/undefined collections** - Use optional chaining (`?.`) and provide fallbacks.

2. **Keep transformations simple** - Complex logic should be broken into helper functions.

3. **Pass transformed data explicitly** - When you modify collection data, pass it via `setProps` rather than relying on automatic injection.

4. **Use descriptive variable names** - Name your processed collections clearly: `displayItems`, `sortedProducts`, `activeFeatures`.

5. **Consider edit mode** - Provide placeholder data when collections are empty during editing.

## Related

- [rw.collections](../hooks.js/available-data/rw.collections.md) - Full collections API reference
- [rw.setProps](../hooks.js/available-functions/rw.setprops.md) - Passing data to templates
- [Accessing Data in Templates](accessing-data-in-templates.md) - Template-side collection usage
- [Collection-Driven Dropzones](../../guides/collection-driven-dropzones.md) - Pairing collections with per-item dropzones
- [Designing the Edit-Mode Experience](../../guides/edit-mode-experience.md) - Placeholder items and preview datasets
