# Spacing



{% hint style="info" %}
**Important:** This documentation is incomplete and missing options.

Check back soon for a complete list.
{% endhint %}

The “mode” key on themeSpacing properties can be set to `padding`, `margin`, `gap`, or `translate` to change the behaviour of the control.

### Spacing Example

You can use the following code as a starting point for adding the padding and gap control.&#x20;

```
{
    "title" : "Padding",
    "properties" : [{
        "title" : "Spacing",
        "property" : "themePadding",
        "themeSpacing": {
            "mode": "padding",
            "default": {
                "custom": false,
                "left" : "sm",
                "right" : "lg",
                "top" : "xl",
                "bottom" : "xs",
                "linkHorizontal": true
            }
        }
    }]
}, {
    "title" : "Gap",
    "properties" : [{
        "title" : "Gap",
        "property" : "themeGap",
        "themeSpacing": {
            "mode": "gap",
            "default": {
                "custom": true,
                "left" : 10,
                "right" : 20,
                "top" : 30,
                "bottom" : 40,
                "linkVertical": true
            }
        }
    }]
}

```
