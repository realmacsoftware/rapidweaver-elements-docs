# Text Area

Displays a multiline text area in the inspector.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Description",
  "id": "cardDescription",
  "textArea": {
    "size": 5,
    "default": "Add a short paragraph that explains the feature."
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Card Content",
    "properties": [{
      "title": "Description",
      "id": "cardDescription",
      "textArea": {
        "size": 5,
        "default": "Add a short paragraph that explains the feature."
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

### Supported Options

The textArea control supports the following options.

| Key       | Type   | Notes                                        |
| --------- | ------ | -------------------------------------------- |
| `default` | string | The default value for the text area.         |
| `size`    | number | The height of the text area, in rows.        |

### Value

In templates, `{{id}}` returns the entered text, with [format](../general-structure/format.md) applied if set. For single-line values use the [Text](text.md) control.
