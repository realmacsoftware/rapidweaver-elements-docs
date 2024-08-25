# Number

Displays a number field with a stepper.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Number",
    "id": "myNumber",
    "number": {
        "default": 100,
        "subtitle": "a simple number input"
    }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "Number Example",
        "properties": [{
            "title": "Number",
            "id": "myNumber",
            "number" : {
                "default" : 100,
                "subtitle" : "a simple number input",
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}
