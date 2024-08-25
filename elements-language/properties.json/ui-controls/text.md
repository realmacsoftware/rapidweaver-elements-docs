# Text

Displays a text field in the inspector.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Text Field",
  "id": "MyTextField",
  "text": {
    "default": "Hello World",
    "subtitle": "one"
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
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
{% endtab %}
{% endtabs %}
