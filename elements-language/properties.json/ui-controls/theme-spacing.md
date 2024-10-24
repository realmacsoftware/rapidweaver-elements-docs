# Theme Spacing

Displays the Theme Studio Spacing control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Padding",
    "id": "themeSpacing",
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
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "Theme Spacing Example",
        "properties": [{
            "title": "Padding",
            "id": "themeSpacing",
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
{% endtab %}
{% endtabs %}

The `themeSpacing` attribute is should be used for all space settings like padding, margins, gaps, translate, and positioning.

This control allows the user's site to dynamically adapt to any theme updates, changes, or overrides to the spacing scale.

The themeSpacing control has the following modes:

* padding
* margin
* gap
* transition
* position
* single

Each one of these modes correspond to the appropriate Tailwind utility classes. This means both developers and users can manage one single spacing scale that help promote consistency across all sites built in RapidWeaver Elements. See the examples below for more information.

```
{
    "groups": [{
        "title": "Theme Spacing Example",
        "properties": [{
            "title": "Padding",
            "id": "themeSpacing",
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

### Single Mode

The single mode allows you to access the spacing scale from the Theme Studio in a single select control. This is handy when you need to set a single property rather than all four properties (top, right, bottom left). For example, if you need to set only the `top` css property you can do so like this:

```
{
    "title": "Top",
    "id": "top",
    "format": "top-{{value}}
    "themeSpacing": {
        "mode": "single",
        "default": {
            "base": {
                "value": "2",
            }
        }
    }
}
```

In this example, the default value will be returned as `top-2`.

### Custom Values

You can also specify that a custom value should be used by default for the themeSpacing control. This allows you to gain precise control over the value of the spacing when your element is dropped on to a page.

### Linking Values
