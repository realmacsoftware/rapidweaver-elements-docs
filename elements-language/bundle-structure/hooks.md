---
description: A powerful and flexible way to extend Elements
---

# Hooks

Global Properties

| Property Name | Type   | Values              |
| ------------- | ------ | ------------------- |
| `rw:mode`     | string | `edit` or `preview` |
|               |        |                     |
|               |        |                     |

Hooks are an incredibly powerful way to extend your Elements, performing heavy manipulations on properties before using them in your templates. Every Element can specify it's own hooks Javascript file, named `hooks.js` and placed in the root directory of the element.

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
<p><strong>%id=obj.name%</strong> - %id=obj.job.title%</p>
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
The slider is %id=padding%
```

When the slider is set to 5, the output would be

```
The slider is 5
```

Now lets add a transform hook that multiplies the padding value by 2

```
const transformHook = (context) => {
  const {
    padding,
  } = context.getValues();

  context.setValues({
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
const transformHook = (context) => {
  const {
    customSizing,     // Checkbox
    size,             // Slider 
    fontSize          // Slider 
    paddingTop        // Slider 
    paddingRight      // Slider 
    paddingBottom     // Slider 
    paddingLeft       // Slider
  } = context.getValues();
  
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
    // Filter out nil items
    .filter(Boolean)
    // Join all items, separating with a space
    .join(" ");

  context.setValues({
    classes: sizeClasses,
  });
};

exports.transformHook = transformHook;
```

The template simply uses the classes property instead of attempting to handle all options from 7 different properties. For example&#x20;

```
<div class="%id=classes%"><div>
```
