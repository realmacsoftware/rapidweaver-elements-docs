# rw.props

The `rw.props` object contains all the current values from your component's UI controls defined in `properties.json`.

{% hint style="info" %}
Values you pass to `rw.setProps()` won't appear in `rw.props` — it always reflects the UI control values. The best pattern is to read everything you need from `rw.props` at the start of your hook, do your work with local variables, and call `rw.setProps()` at the end.
{% endhint %}

## Accessing Properties

Use destructuring to access individual property values:

```javascript
const transformHook = (rw) => {
    const { title, isVisible, padding, backgroundColor } = rw.props;
    
    // Use the values
    console.log(title);       // "My Component"
    console.log(isVisible);   // true
    console.log(padding);     // 16
};

exports.transformHook = transformHook;
```

## Property Types

The type of each property matches how it's defined in `properties.json`:

| Control Type | JavaScript Type | Example Value |
|--------------|-----------------|---------------|
| Text | `string` | `"Hello World"` |
| Number / Slider | `number` | `42` |
| Switch | `boolean` | `true` |
| Select / Segmented | `string` | `"option1"` |
| Color | `string` | `"bg-blue-500"` |
| Image / Resource | `object` | `{ image: "path/to/image.jpg", width: 800, height: 600 }` |
| Link | `object` | `{ href: "/page", title: "Link", target: "_self" }` |

## Example: Transforming Properties

```javascript
const transformHook = (rw) => {
    const { 
        firstName, 
        lastName, 
        showFullName,
        fontSize 
    } = rw.props;
    
    // Combine properties
    const displayName = showFullName 
        ? `${firstName} ${lastName}` 
        : firstName;
    
    // Transform values
    const fontSizeClass = `text-${fontSize}`;
    
    rw.setProps({
        displayName,
        fontSizeClass
    });
};

exports.transformHook = transformHook;
```

## All Properties Available

Every property defined in your `properties.json` is accessible via `rw.props`. If a property has a `default` value and hasn't been changed, the default value will be returned.

```javascript
const transformHook = (rw) => {
    // Log all available properties
    console.log(rw.props);
    
    // Access any property by its "property" key from properties.json
    const { myCustomProperty } = rw.props;
};

exports.transformHook = transformHook;
```
