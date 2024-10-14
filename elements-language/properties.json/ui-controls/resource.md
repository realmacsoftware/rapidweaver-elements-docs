# Resource

Displays a resource dropwell that accepts all file types.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Resource",
    "id": "resource",
    "resource": {}
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "Resource Example",
        "icon": "folder",
        "properties": [{
            "title": "Resource",
            "id": "resource",
            "resource": {}
        }]
    }]
}
```
{% endtab %}
{% endtabs %}

### Restricting File Types

You can restrict the file types allowed in a dropwell, by using the `accepts` property.

```json
"resource": {
    "accepts": "svg"
}
```

Support for multiple file types can be added using comma seperated values.

```json
"resource": {
    "accepts": "zip, pdf"
}
```



