# Theme Typography

Displays the Theme Studio Typography class picker.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Article Style",
  "id": "articleStyle",
  "themeTypography": {
    "default": {
      "base": {
        "name": "article"
      },
      "md": {
        "name": "article-lg"
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
      "title": "Article Style",
      "id": "articleStyle",
      "themeTypography": {
        "default": {
          "base": {
            "name": "article"
          },
          "md": {
            "name": "article-lg"
          }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

Typography classes style a whole block of content at once — headings, paragraphs, lists, and links inside the element — making this control a good fit for components that render rich or markdown content.

### Supported Options

The themeTypography control supports the following options.

| Key       | Type   | Notes                                                                                                                     |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------ |
| `default` | object | Per-breakpoint defaults (`base`, `sm`, `md`, …). Each breakpoint holds the `name` of a typography class from the theme, e.g. `{ "name": "article" }`. |

### Value

In templates, `{{id}}` outputs the classes for the selected typography preset, prefixed for each breakpoint the user has configured. For styling a single piece of text, use [Theme Text Style](theme-text-style.md) instead.
