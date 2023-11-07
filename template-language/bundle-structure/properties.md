# Properties

properties.json

{% hint style="info" %}
Icon type is an SF Symbol. This control does not support Font Awesome.
{% endhint %}

```
{
    "groups": [{
        "title" : "Formatting",
        "icon": "textformat.size",
        "properties" : [{
            "title": "Alignment",
            "property": "alignment",
            "segmented": {
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
