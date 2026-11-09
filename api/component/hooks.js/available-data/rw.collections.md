# rw.collections

The `rw.collections` object contains all collections defined for your component. Collections are arrays of structured data items that users can add, edit, and reorder.

## Accessing Collections

```javascript
const transformHook = (rw) => {
    const { tags, items, slides } = rw.collections;
    
    // Each collection is an array
    console.log(tags);   // [{ title: "Tag 1" }, { title: "Tag 2" }]
    console.log(items);  // [{ name: "Item 1", price: 10 }, ...]
};

exports.transformHook = transformHook;
```

## Working with Collection Data

### Mapping Collection Items

```javascript
const transformHook = (rw) => {
    const { tags } = rw.collections;
    
    // Create a comma-separated list of tag names
    const tagList = tags.map(tag => tag.title).join(", ");
    
    rw.setProps({
        tagList
    });
};

exports.transformHook = transformHook;
```

### Filtering Collections

```javascript
const transformHook = (rw) => {
    const { products } = rw.collections;
    
    // Filter to only featured products
    const featuredProducts = products.filter(p => p.isFeatured);
    
    // Calculate total
    const totalPrice = products.reduce((sum, p) => sum + p.price, 0);
    
    rw.setProps({
        featuredProducts,
        totalPrice
    });
};

exports.transformHook = transformHook;
```

### Passing Collections to Templates

You can pass individual collections or spread all collections:

```javascript
const transformHook = (rw) => {
    // Pass all collections to the template
    rw.setProps({
        ...rw.collections
    });
};

exports.transformHook = transformHook;
```

Or pass specific collections:

```javascript
const transformHook = (rw) => {
    const { items, categories } = rw.collections;
    
    rw.setProps({
        items,
        categories,
        itemCount: items.length
    });
};

exports.transformHook = transformHook;
```

## Using Collections in Templates

Once passed via `setProps`, collections can be iterated in templates:

```html
@each(item in items)
    <div class="item">
        <h3>{{item.title}}</h3>
        <p>{{item.description}}</p>
    </div>
@endeach
```

## Collection Item Properties

Each item in a collection has the properties defined in your collection schema. Common patterns include:

```javascript
const transformHook = (rw) => {
    const { slides } = rw.collections;
    
    slides.forEach((slide, index) => {
        // Access item properties
        console.log(slide.title);
        console.log(slide.image);
        console.log(slide.link);
        
        // Add computed properties
        slide.isFirst = index === 0;
        slide.isLast = index === slides.length - 1;
    });
    
    rw.setProps({ slides });
};

exports.transformHook = transformHook;
```
