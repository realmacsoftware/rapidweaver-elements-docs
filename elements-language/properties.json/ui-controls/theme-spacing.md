# Theme Spacing

{% hint style="info" %}
**Important:** This documentation is incomplete and missing options.

Check back soon for a complete list.
{% endhint %}

The `themeSpacing` attribute is should be used for all space settings like padding, margins, gaps, translate, and positioning.

This control allows the user's site to dynamically adapt to any theme updates, changes, or overrides to the spacing scale.

The themeSpacing control has the following modes:

* padding
* margin
* gap
* transition
* position

Each one of these modes correspond to the appropriate Tailwind utility classes. This means both developers and users can manage one single spacing scale that help promote consistency across all sites built in RapidWeaver Elements. See the examples below for more information.

```
{
    "groups": [{
        "title": "Theme Spacing Example",
        "properties": [{
            "title": "Padding",
            "property": "themeSpacing",
            "themeSpacing": {
                "mode": "padding",
                "default": {
                    "base": {
                        "left": "sm",
                        "right": "sm",
                        "top": "sm",
                        "bottom": "sm"
                    },
                    "md": {
                        "left": "md",
                        "right": "md",
                        "top": "md",
                        "bottom": "md"
                    }
                }
            }
        }]
    }]
}
```

### Custom Values

You can also specify that a custom value should be used by default for the themeSpacing control. This allows you to gain precise control over the value of the spacing when your element is dropped on to a page.

### Linking Values
