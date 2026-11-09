# Input

Displays a compact single-line input field. It works like the [Text](text.md) control but is suited to short technical values — numbers, comma-separated lists, or code-like strings — rather than sentences of content.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Cubic Bezier",
  "id": "timingFunctionCustom",
  "format": "ease-[cubic-bezier({{value}})]",
  "input": {
    "default": "0.95,0.05,0.795,0.035",
    "subtitle": "x1, y1, x2, y2"
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Transition",
    "properties": [{
      "title": "Cubic Bezier",
      "id": "timingFunctionCustom",
      "format": "ease-[cubic-bezier({{value}})]",
      "input": {
        "default": "0.95,0.05,0.795,0.035",
        "subtitle": "x1, y1, x2, y2"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

### Supported Options

The input control supports the following options.

| Key        | Type   | Notes                                            |
| ---------- | ------ | ------------------------------------------------ |
| `default`  | string | The default value for the field.                 |
| `subtitle` | string | Helper text displayed underneath the field.      |

### Value

In templates, `{{id}}` returns the entered string, with [format](../general-structure/format.md) applied if set. In the example above the default value renders as `ease-[cubic-bezier(0.95,0.05,0.795,0.035)]`.

### Hidden Properties

An input combined with `"visible": "false"` is a handy way to store a constant value that other properties can reference in their [visible](../general-structure/visible.md) or [enable](../general-structure/enabled.md) expressions:

```json
{
  "title": "Background Type",
  "id": "backgroundType",
  "visible": "false",
  "input": {
    "default": "static"
  }
}
```
