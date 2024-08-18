# Text

A text field can be used for freeform text input.

### Text Field

The following code example will display a text field inside of a group.

```
{
    "groups": [{
        "title": "Text Field Example",
        "properties": [{
            "title": "Text Field",
            "property": "MyTextField",
            "text": {
                "default" : "Hello World",
                "subtitle" : "one",
            }
        }]
    }]
}
```

The following code example for the Text Field control should be placed inside of the main ‘properties’ array which is inside of groups, see [Grouping Controls](../grouping-controls.md).

```
{
            "title": "Text Field",
            "property": "MyTextField",
            "text": {
                "default" : "Hello World",
                "subtitle" : "one",
            }
        }
```
