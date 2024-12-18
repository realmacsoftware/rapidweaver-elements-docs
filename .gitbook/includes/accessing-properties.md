---
title: Accessing Properties
---

## Accessing Properties

[UI Control Properties](../../elements-language/properties.json/ui-controls/) can be placed inside of HTML, CSS, and Javascript files.

For example in your [Properties.json](../../elements-language/properties.json/) file you can add the a [text field](../../elements-language/properties.json/ui-controls/text.md), and then reference that value in your [Template files](../../elements-language/templates/), including HTML, CSS, and Javascript.

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

