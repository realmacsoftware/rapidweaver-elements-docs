# Number

Displays a number field with a stepper.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Max Items",
  "id": "maxItems",
  "number": {
    "default": 6,
    "subtitle": "Number of cards to show"
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Collection Settings",
    "properties": [{
      "title": "Max Items",
      "id": "maxItems",
      "number": {
        "default": 6,
        "subtitle": "Number of cards to show"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

The following example constrains the value to a range and steps in increments:

```json
{
  "title": "Columns",
  "id": "gridColumns",
  "format": "grid-cols-{{value}}",
  "number": {
    "default": 3,
    "min": 1,
    "max": 12,
    "step": 1
  }
}
```

### Supported Options

The number control supports the following options.

| Key        | Type    | Notes                                                         |
| ---------- | ------- | ------------------------------------------------------------- |
| `default`  | number  | The default value for the field.                              |
| `min`      | number  | The minimum value that can be entered.                        |
| `max`      | number  | The maximum value that can be entered.                        |
| `step`     | number  | The amount the stepper increments or decrements the value by. |
| `round`    | boolean | If true an integer will be used instead of a floating point.  |
| `subtitle` | string  | Helper text displayed underneath the field.                   |

### Value

In templates, `{{id}}` returns the entered number, with [format](../general-structure/format.md) applied if set. For choosing from a range with a draggable handle, use the [Slider](slider.md) control instead.
