# Theme Font

Displays the Theme Studio Font control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Headline Font",
  "id": "headlineFont",
  "themeFont": {
    "default": {
      "base": { "name": "heading" },
      "sm": { "name": "heading" },
      "md": { "name": "display" }
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
      "title": "Headline Font",
      "id": "headlineFont",
      "themeFont": {
        "default": {
          "base": { "name": "heading" },
          "sm": { "name": "heading" },
          "md": { "name": "display" }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

For effective theme integration in RapidWeaver Elements, it is recommended to use the `themeFont` attribute to define all font family settings for your elements. This approach ensures that font preferences are coordinated with the overall theme settings, providing a consistent user experience.

### Supported Options

The themeFont control supports the following options.

| Key       | Type   | Notes                                                                                                             |
| --------- | ------ | -------------------------------------------------------------------------------------------------------------------- |
| `default` | object | Per-breakpoint defaults (`base`, `sm`, `md`, …). Each breakpoint holds the `name` of a font from the theme, e.g. `{ "name": "heading" }`. |

### Value

In templates, `{{id}}` outputs the font utility classes for the selected theme font, prefixed for each breakpoint the user has configured. With the example configuration above, referencing `{{headlineFont}}` would output: `font-heading sm:font-heading md:font-display`.
