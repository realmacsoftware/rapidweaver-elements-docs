# Divider

Display a divider between content. Use it to visually separate runs of related controls within a [group](../grouping-controls.md). The control takes no options, stores no value, and needs no `id` or `title`.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "divider": {}
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Card Settings",
    "properties": [{
      "title": "Content",
      "heading": {}
    }, {
      "title": "Title",
      "id": "cardTitle",
      "text": {
        "default": "New arrivals"
      }
    }, {
      "divider": {}
    }, {
      "title": "Button",
      "heading": {}
    }, {
      "title": "Button Label",
      "id": "buttonLabel",
      "text": {
        "default": "Shop now"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
