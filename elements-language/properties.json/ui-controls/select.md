# Select

Displays a select box, also known as a dropdown menu.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Case",
    "id": "headingTextTransform",
    "select": {
        "default": "normal-case",
        "items": [
            {
                "value": "normal-case",
                "title": "None"
            },
            {
                "value": "uppercase",
                "title": "Uppercase"
            },
            {
                "value": "lowercase",
                "title": "Lowercase"
            },
            {
                "value": "capitalize",
                "title": "Capitalize"
            }
        ]
    }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "Select Example",
        "properties": [ {
            "title": "Case",
            "id": "headingTextTransform",
            "select": {
                "default": "normal-case",
                "items": [{
                    "value": "normal-case",
                    "title": "None"
                }, {
                    "value": "uppercase",
                    "title": "Uppercase"
                }, {
                    "value": "lowercase",
                    "title": "Lowercase"
                }, {
                    "value": "capitalize",
                    "title": "Capitalize"
                }]
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}
