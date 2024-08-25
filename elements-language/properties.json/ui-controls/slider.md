# Slider

A slider can be used for choosing from a range of values.

Displays a resource dropwell.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Resource",
    "id": "resource",
    "resource": {}
}
```
{% endtab %}

{% tab title="Group Example" %}
The following example displays a stepped slider with seven pre-defined values.

```json


{
    "groups": [{
        "title": "Slider Example",
        "properties": [{
            "title": "Contrast",
            "id": "contrast",
            "slider": {
                "default": "contrast-70",
                "items": [
                    { "value": "contrast-0", "title": "0" },
                    { "value": "contrast-50", "title": "50" },
                    { "value": "contrast-70", "title": "75" },
                    { "value": "contrast-100", "title": "100" },
                    { "value": "contrast-125", "title": "125" },
                    { "value": "contrast-150", "title": "150" },
                    { "value": "contrast-200", "title": "200" }
                ]
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}





### Supported Options <a href="#key-value-pairs-explained" id="key-value-pairs-explained"></a>

The slider control supports the following options.

| Key       | Type    | Notes                                                                                                                                                                                       |
| --------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title`   | string  | The name of the Slider. This will be displayed beside the UI element of RapidWeaver                                                                                                         |
| `id`      | string  | The id for this control.                                                                                                                                                                    |
| `format`  | string  | Can be used to apply additional formatting to the value. `{{value}}` will be replaced with the selected value. See [value formatting](../general-structure/format.md) for more information. |
| `default` | string  | The default value the slider should be set to.                                                                                                                                              |
| `items`   | array   | Can be used to specify an array of values to the slider. See [code example](slider.md#slider-example) below.                                                                                |
| `min`     | number  | The minimum value for the slider.                                                                                                                                                           |
| `max`     | number  | The maximum value for the slider.                                                                                                                                                           |
| `units`   | string  | The units string appears alongside the slider value in the user interface, but it is not included in the template output value.                                                             |
| `round`   | boolean | If true an integer will be used instead of a floating point.                                                                                                                                |
| `ticks`   | number  | the number of ticks that will appear beneath the slider                                                                                                                                     |

### Slider Example

You can use the following code as a starting point for a stepped slider with seven values.

```
{
    "groups": [{
        "title": "Slider Example",
        "properties": [{
            "title": "Contrast",
            "id": "contrast",
            "slider": {
                "default": "contrast-70",
                "items": [
                    { "value": "contrast-0", "title": "0" },
                    { "value": "contrast-50", "title": "50" },
                    { "value": "contrast-70", "title": "75" },
                    { "value": "contrast-100", "title": "100" },
                    { "value": "contrast-125", "title": "125" },
                    { "value": "contrast-150", "title": "150" },
                    { "value": "contrast-200", "title": "200" }
                ]
            }
        }]
    }]
}
```

The following example has a minimum value of 0 and maximum of 100. The units are set to round, and display in the UI with a "%" after the number.

```
{
    "groups": [{
        "title": "Slider Example",
        "properties": [{
            "title": "Contrast",
            "id": "contrast",
            "format": "{{value}}%",
            "slider": {
                "default": 50,
                "min": 0,
                "max": 100,
                "units": "%",
                "round": true
            }
        }]
    }]
}
```

An example slider setting a star rating between 0 and 5.

```
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

```
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
