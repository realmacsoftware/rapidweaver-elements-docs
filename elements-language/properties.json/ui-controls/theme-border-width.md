# Theme Border Width

Displays the Theme Studio Border Width control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Border",
    "id": "borderWidth",
    "themeBorderWidth": {
        "default": {
            "base": {
                "top": "2",
                "right": "2",
                "bottom": "2",
                "left": "2"
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
        "title": "Theme Border Example",
        "properties": [{
            "title": "Border",
            "id": "borderWidth",
            "themeBorderWidth": {
                "default": {
                    "base": {
                        "top": "2",
                        "right": "2",
                        "bottom": "2",
                        "left": "2"
                    }
                }
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}
