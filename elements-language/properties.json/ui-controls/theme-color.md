# Theme Color

Displays the Theme Studio Color control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Color",
  "id": "customColor",
  "format": "text-{{value}}",
  "themeColor": {
    "default": {
      "name": "blue",
      "brightness": 600
    }
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "Theme Color Example",
        "properties": [{
            "title": "Color",
            "id": "customColor",
            "format": "text-{{value}}",
            "themeColor": {
                "default": {
                    "name": "blue",
                    "brightness": 600
                }
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}

For consistency and integration with the Theme Studio in RapidWeaver Elements, use the `themeColor` attribute to specify all color options for your elements. This ensures that the color settings are centrally managed and adaptable to theme changes.

**Usage of `themeColor`:**

* **default**: Sets the initial or fallback color and brightness. In this case, the default color is black with a brightness value of 300.

**Output Example:** [The `format` key](../general-structure/format.md) controls the output format of the `customColor` property. In your template files, referencing `{{customColor}}` with the example configuration above would output: `text-black-300`.
