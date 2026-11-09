# Theme Text Style

Displays the Theme Studio Text Style control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Heading Size",
  "id": "headingTextStyle",
  "themeTextStyle": {
    "default": {
      "base": {
        "name": "3xl"
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
    "title": "Typography",
    "properties": [{
      "title": "Heading Size",
      "id": "headingTextStyle",
      "themeTextStyle": {
        "default": {
          "base": {
            "name": "3xl"
          }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

### Supported Options

The themeTextStyle control supports the following options.

| Key       | Type   | Notes                                                                                                                |
| --------- | ------ | ----------------------------------------------------------------------------------------------------------------------- |
| `default` | object | Per-breakpoint defaults (`base`, `sm`, `md`, …). Each breakpoint holds the `name` of a text style from the theme, e.g. `{ "name": "3xl" }`. |

### Value

In templates, `{{id}}` outputs the utility classes for the selected theme text style, prefixed for each breakpoint the user has configured. Text styles combine size, line height, and other typographic settings defined in Theme Studio. For complete typographic presets covering nested content, see [Theme Typography](theme-typography.md).
