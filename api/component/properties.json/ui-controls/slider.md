# Slider

A slider can be used for choosing from a range of values.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Overlay Opacity",
  "id": "overlayOpacity",
  "format": "bg-opacity-[{{value}}%]",
  "slider": {
    "default": 60,
    "min": 0,
    "max": 100,
    "round": true,
    "units": "%"
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
The following example shows an opacity control for a hero overlay.

```json
{
  "groups": [{
    "title": "Hero Background",
    "properties": [{
      "title": "Overlay Opacity",
      "id": "overlayOpacity",
      "format": "bg-opacity-[{{value}}%]",
      "slider": {
        "default": 60,
        "min": 0,
        "max": 100,
        "round": true,
        "units": "%"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

The following example displays a stepped slider for image brightness.

```json
{
  "groups": [{
    "title": "Image Effects",
    "properties": [{
      "title": "Brightness",
      "id": "imageBrightness",
      "format": "brightness-[{{value}}%]",
      "slider": {
        "default": 100,
        "items": [
          { "value": "50", "title": "50" },
          { "value": "75", "title": "75" },
          { "value": "100", "title": "100" },
          { "value": "125", "title": "125" },
          { "value": "150", "title": "150" }
        ]
      }
    }]
  }]
}
```

An example slider setting a star rating between 0 and 5.

```json
{
    "groups": [{
        "title": "Slider Example",
        "properties": [{
            "title": "Rating",
            "id": "rating",
            "slider": {
                "default": 3,
                "min": 0,
                "max": 5,
                "round": true,
                "units": "Stars",
                "ticks": 6
            }
        }]
    }]
}
```

Here's an example of an `items` array in sliders so you can set custom values for each point in the slider.

```json
{
    "groups": [{
        "title": "Slider Example",
        "properties": [{
            "title": "Z Index",
            "id": "zIndex",
            "format": "z-{{value}}",
            "slider": {
                "default": "0",
                "items": [{
                    "value": "0",
                    "title": "0"
                }, {
                    "value": "10",
                    "title": "10"
                }, {
                    "value": "20",
                    "title": "20"
                }, {
                    "value": "30",
                    "title": "30"
                }, {
                    "value": "40",
                    "title": "40"
                }, {
                    "value": "50",
                    "title": "50"
                }]
            }
        }]
    }]
}
```

### Supported Options <a href="#key-value-pairs-explained" id="key-value-pairs-explained"></a>

The slider control supports the following options.

| Key       | Type    | Notes                                                                                                                                                                                       |
| --------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title`   | string  | The name of the Slider. This will be displayed beside the UI element of RapidWeaver                                                                                                         |
| `id`      | string  | The id for this control.                                                                                                                                                                    |
| `format`  | string  | Can be used to apply additional formatting to the value. `{{value}}` will be replaced with the selected value. See [value formatting](../general-structure/format.md) for more information. |
| `default` | number  | The default value the slider should be set to. A string when using `items`, an object when setting per-breakpoint defaults (see [Default Values](../default-values.md)).                   |
| `items`   | array   | Can be used to specify an array of values to the slider. See [code example](slider.md#slider-example) below.                                                                                |
| `min`     | number  | The minimum value for the slider.                                                                                                                                                           |
| `max`     | number  | The maximum value for the slider.                                                                                                                                                           |
| `step`    | number  | The amount the value changes per increment as the slider is dragged.                                                                                                                        |
| `units`   | string  | The units string appears alongside the slider value in the user interface, but it is not included in the template output value.                                                             |
| `round`   | boolean | If true an integer will be used instead of a floating point.                                                                                                                                |
| `ticks`   | number  | the number of ticks that will appear beneath the slider.                                                                                                                                    |
| `snap`    | boolean | is set to true, slider will snap to `ticks`.                                                                                                                                                |

### Value

In templates, `{{id}}` returns the selected number (or the matching item's `value` when using `items`), with [format](../general-structure/format.md) applied if set. In the opacity example above the default renders as `bg-opacity-[60%]`.

