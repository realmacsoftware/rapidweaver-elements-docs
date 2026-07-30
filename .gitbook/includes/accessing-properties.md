---
title: Accessing Properties
---

[UI Control Properties](https://docs.realmacsoftware.com/elements-docs/elements-language/component/properties-json) can be placed inside any template file, including HTML, CSS, and JavaScript files.

For example, in your [properties.json](https://docs.realmacsoftware.com/elements-docs/elements-language/component/properties-json) file you can add a text field, then reference that value in your [template files](https://docs.realmacsoftware.com/elements-docs/elements-language/component/templates), including HTML, CSS, and JavaScript.

```json
{
    "groups": [{
        "title": "Text Field Example",
        "properties": [{
            "title": "Text Field",
            "id": "MyTextField",
            "text": {
                "default" : "Hello World",
                "subtitle" : "one",
            }
        }]
    }]
}
```

In your Template file you can reference the text field by using double brackets and the ID name.

```html
<h1>This is the value from the Text Field: {{MyTextField}}</h1>
```

{% hint style="info" %}
Anything set with [rw.setProps](https://docs.realmacsoftware.com/elements-docs/elements-language/component/hooks.js/passing-data-to-templates) is also available to every template file in your component.
{% endhint %}
