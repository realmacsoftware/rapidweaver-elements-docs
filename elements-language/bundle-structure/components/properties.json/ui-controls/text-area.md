# Text Area

Displays a multiline text area in the inspector.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "TextArea",
    "id": "myTextArea",
    "textArea": {
        "size": 5,
        "default": "Hello World"
    }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "TextArea Example",
        "properties": [{
            "title": "TextArea",
            "id": "myTextArea",
            "textArea": {
                "size": 5,
                "default": "Hello World"
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}
