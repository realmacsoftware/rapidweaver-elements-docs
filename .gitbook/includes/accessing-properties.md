---
title: Accessing Properties
---

## Accessing Properties

[UI Control Properties](../../elements-language/bundle-structure/components/properties.json/ui-controls/) can be placed inside of any Template files, including HTML, CSS, and Javascript files.

For example in your [Properties.json](../../elements-language/bundle-structure/components/properties.json/) file you can add the a [text field](../../elements-language/bundle-structure/components/properties.json/ui-controls/text.md), and then reference that value in your [Template files](../../elements-language/bundle-structure/components/templates/), including HTML, CSS, and Javascript.

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
Anything set in [rw.setProps](../../elements-language/bundle-structure/components/hooks.js/available-data/rw.props.md) is also available to all Templates files in your component.
{% endhint %}

