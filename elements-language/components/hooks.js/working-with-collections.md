# Working with Collections



```
const transformHook = (rw) => {
    rw.setProps({
        // Very important to have access to the collections in the template.
        ...rw.collections
    })
}
exports.transformHook = transformHook;
```

