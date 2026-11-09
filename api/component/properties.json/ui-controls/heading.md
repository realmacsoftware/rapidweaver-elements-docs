# Heading

Displays a heading in the inspector interface. Use it to label a sub-section of controls within a [group](../grouping-controls.md). The heading text comes from the property's `title` — the control itself takes no options, stores no value, and needs no `id`.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Typography",
  "heading": {}
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Text Styles",
    "properties": [{
      "title": "Typography",
      "heading": {}
    }, {
      "title": "Text Style",
      "id": "textStyle",
      "themeTextStyle": {
        "default": {
          "base": {
            "name": "lg"
          }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
