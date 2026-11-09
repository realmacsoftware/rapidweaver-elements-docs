# Text

Displays a text field in the inspector.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Button Label",
  "id": "buttonLabel",
  "text": {
    "default": "Get Started",
    "subtitle": "Short call-to-action"
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Button",
    "properties": [{
      "title": "Button Label",
      "id": "buttonLabel",
      "text": {
        "default": "Get Started",
        "subtitle": "Short call-to-action"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

### Supported Options

The text control supports the following options.

| Key           | Type   | Notes                                                  |
| ------------- | ------ | ------------------------------------------------------ |
| `default`     | string | The default value for the field.                       |
| `placeholder` | string | Placeholder text shown while the field is empty.       |
| `subtitle`    | string | Helper text displayed underneath the field.            |

### Value

In templates, `{{id}}` returns the entered string, with [format](../general-structure/format.md) applied if set. For multiline content use the [Text Area](text-area.md) control, and for short technical values consider the [Input](input.md) control.
