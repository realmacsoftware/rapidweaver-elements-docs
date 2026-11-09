# Segmented

Display a segmented control.&#x20;

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Button Style",
  "id": "buttonStyle",
  "segmented": {
    "default": "solid",
    "items": [{
      "value": "solid",
      "icon": "rectangle.fill"
    }, {
      "value": "outline",
      "icon": "rectangle"
    }, {
      "value": "ghost",
      "icon": "square.dashed"
    }]
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
      "title": "Button Style",
      "id": "buttonStyle",
      "segmented": {
        "default": "solid",
        "items": [{
          "value": "solid",
          "icon": "rectangle.fill"
        }, {
          "value": "outline",
          "icon": "rectangle"
        }, {
          "value": "ghost",
          "icon": "square.dashed"
        }]
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

You can also use the following title key to display text instead of icons.

```json
{
  "groups": [{
    "title": "Layout",
    "properties": [{
      "title": "Content Alignment",
      "id": "contentAlignment",
      "segmented": {
        "items": [{
          "value": "text-left",
          "title": "Left"
        }, {
          "value": "text-center",
          "title": "Center",
          "default": true
        }, {
          "value": "text-right",
          "title": "Right"
        }]
      }
    }]
  }]
}
```

### Supported Options

The segmented control supports the following options.

| Key       | Type   | Notes                                                                                                       |
| --------- | ------ | ----------------------------------------------------------------------------------------------------------- |
| `default` | string | Value of the segment selected by default. An object of per-breakpoint values when the control is responsive. |
| `items`   | array  | The segments to display. See the item schema below.                                                          |

Each item in `items` supports these keys:

| Key       | Type    | Notes                                                                                       |
| --------- | ------- | -------------------------------------------------------------------------------------------- |
| `value`   | string  | The value to be returned when this segment is selected.                                      |
| `title`   | string  | The text label for the segment.                                                              |
| `icon`    | string  | An [SF Symbol](https://developer.apple.com/sf-symbols/) name to display instead of a label.  |
| `default` | boolean | Alternative way to mark this item as the default selection.                                  |

### Value

The segmented control works like [Select](select.md): when responsive it returns Tailwind classes prefixed per breakpoint, and when `responsive` is `false` it returns the selected item's raw `value`. [Format](../general-structure/format.md) is applied if set.
