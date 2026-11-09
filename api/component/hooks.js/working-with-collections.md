# Working with Collections

All collections that have been setup for a component are available via the `rw.collections` object. Assuming we have a tags collection setup, you can do the following:

```javascript
const transformHook = (rw) => {
    const { tags } = rw.collections;

    // Example: Create an array of tag names
    const tagNames = tags.map(tag => tag.name);

    rw.setProps({
        tagNames
    });
}
exports.transformHook = transformHook;
```

If you want like to simple pass all the collections to the template, you can do so by spreading the `rw.collections` object into the `rw.setProps` method, like so

```javascript
const transformHook = (rw) => {
    rw.setProps({
        ...rw.collections
    });
}
exports.transformHook = transformHook;
```
