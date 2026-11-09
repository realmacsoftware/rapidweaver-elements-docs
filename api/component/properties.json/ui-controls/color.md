# Color

Displays a color picker that stores a raw hex value.

{% hint style="info" %}
For most color settings you should use the [Theme Color](theme-color.md) control instead — it keeps colors managed by Theme Studio so sites adapt to theme changes and dark mode automatically. Reserve the raw `color` control for cases where a fixed hex value is genuinely required, such as configuring a third-party library that only accepts hex colors.
{% endhint %}

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Toolbar Background",
  "id": "toolbarBackground",
  "color": {
    "default": "#F9F9FA"
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Viewer Appearance",
    "properties": [{
      "title": "Toolbar Background",
      "id": "toolbarBackground",
      "color": {
        "default": "#F9F9FA"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

### Supported Options

The color control supports the following options.

| Key       | Type   | Notes                                        |
| --------- | ------ | -------------------------------------------- |
| `default` | string | The default color as a hex string, e.g. `#D4D4D7`. |

### Value

In templates, `{{id}}` returns the selected hex string. Unlike the [Theme Color](theme-color.md) control there is no built-in light/dark pairing — if a component needs a separate dark-mode color, define a second property for it:

```json
{
  "title": "Background",
  "id": "backgroundColor",
  "color": { "default": "#D4D4D7" }
},
{
  "title": "Background (Dark)",
  "id": "backgroundColorDark",
  "color": { "default": "#2A2A2E" }
}
```
