---
icon: anchor
---

# Hooks.js

Hooks provide a powerful way to extend your components by manipulating properties before they are applied within templates.

The typical flow of a component follows this sequence: properties → hooks → template. Hooks process and refine properties, allowing you to perform complex logic before passing them into the template for rendering.

{% hint style="info" %}
Each component has its own unique `hooks.js` file. To share code across multiple components, refer to [shared hooks](../shared-files/hooks.md).
{% endhint %}

To use a transform hook, create a `hooks.js`file in the root of your component with this code.

```javascript
// Create a function called transformHook that receives the rw API object
const transformHook = (rw) => {

    // Use the API to set a property called message to "Hooks are awesome!"
    rw.setProps({
        message: "Hooks are awesome!"
    });
};

// Register the transformHook function with Elements
exports.transformHook = transformHook;
```

Next, add this to the `template.html` file in the component templates directory.

```html
<div class="p-6 text-black-600 text-center">
    {{message}}
</div>
```





### Global Properties

<table><thead><tr><th>Property Name</th><th width="186">Type</th><th>Values</th></tr></thead><tbody><tr><td><code>rw:mode</code></td><td>string</td><td><code>edit</code> or <code>preview</code></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

### **Available Context methods**

<table><thead><tr><th>Method Name</th><th width="186">Type</th><th>Values</th></tr></thead><tbody><tr><td><code>getValues</code></td><td></td><td></td></tr><tr><td><code>getClassNames</code></td><td></td><td></td></tr><tr><td><code>getResponsiveValues</code></td><td></td><td></td></tr><tr><td><code>getBreakpoints</code></td><td></td><td></td></tr><tr><td><code>getBreakpointNames</code></td><td></td><td></td></tr></tbody></table>

### Setting Values

in hooks.js

```
// Set values in the context
context.setValues({
    "obj": {
        "name" : "Mario",
        "job" : {
            "title" : "Plumber"
        }
    }
})
```

in template.html

```
<p><strong>{{obj.name}}</strong> - {{obj.job.title}}</p>
```

The rendered output would look something like this:

**Mario** - Plumber



### Transform Hook

The transform hook allows you to get and set property values before they're used in templates. Let's assume you have the following slider defined in your properties and you're using the value in a template.

```
// properties.json
{
    "title" : "Padding",
    "property" : "padding",
    "default" : 5,
    "slider": {
        "min" : 0,
        "max" : 12,
        "round" : true
    }
}
```

```
// template.html
The slider is {{padding}}
```

When the slider is set to 5, the output would be

```
The slider is 5
```

Now lets add a transform hook that multiplies the padding value by 2

```
const transformHook = (rw) => {
  const {
    padding,
  } = rw.props;

  rw.setProps({
    padding: padding*2,
  });
};

exports.transformHook = transformHook;

```

With the slider still set to 5, when the template is processed the output will be

```
The slider is 10
```

This becomes incredibly powerful and convenient when you need to perform logic based on multiple properties. The following example show how you might generate a list of css classes based on standard or custom settings.

```
const transformHook = (rw) => {
  const {
    customSizing,     // Checkbox
    size,             // Slider 
    fontSize          // Slider 
    paddingTop        // Slider 
    paddingRight      // Slider 
    paddingBottom     // Slider 
    paddingLeft       // Slider
  } = rw.props;
  
  const sizeClasses = [
    // Included if customSizing == false
    !customSizing && size,
    
    // Included if customSizing == true
    customSizing && fontSize,
    customSizing && paddingTop,
    customSizing && paddingRight,
    customSizing && paddingBottom,
    customSizing && paddingLeft,
  ]
    .filter(Boolean)
    .join(" ");

  rw.setProps({
    classes: sizeClasses,
  });
};

exports.transformHook = transformHook;
```

The template simply uses the classes property instead of attempting to handle all options from 7 different properties. For example&#x20;

```
<div class="{{classes}}"><div>
```
