# Theme Border Radius

Displays the Theme Studio Border Radius control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Radius",
  "id": "borderRadius",
  "themeBorderRadius": {
    "default": {
      "base": {
        "topRight": "lg",
        "topLeft": "lg",
        "bottomRight": "lg",
        "bottomLeft": "lg"
      }
    }
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "Theme Border Radius Example",
        "properties": [{
            "title": "Radius",
            "id": "borderRadius",
            "themeBorderRadius": {
                "default": {
                    "base": {
                        "topRight": "lg",
                        "topLeft": "lg",
                        "bottomRight": "lg",
                        "bottomLeft": "lg"
                    }
                }
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}
