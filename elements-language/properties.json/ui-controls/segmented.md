# Segmented

Display a segmented control.&#x20;

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Alignment",
    "id": "alignment",
    "segmented": {
        "default": {
            "base": "align-left",
            "md": "align-center"
        },
        "items": [{
            "value": "align-left",
            "icon": "text.alignleft"
        }, {
            "value": "align-center",
            "icon": "text.aligncenter",
            "default": true
        }, {
            "value": "align-right",
            "icon": "text.alignright",
            "title": "Right"
        }]  
    }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "Segmented Example",
        "properties": [{
            "title": "Alignment",
            "id": "alignment",
            "segmented": {
                "default": {
                    "base": "align-left",
                    "md": "align-center"
                },
                "items": [{
                    "value": "align-left",
                    "icon": "text.alignleft"
                }, {
                    "value": "align-center",
                    "icon": "text.aligncenter",
                    "default": true
                }, {
                    "value": "align-right",
                    "icon": "text.alignright",
                    "title": "Right"
                }]  
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}

