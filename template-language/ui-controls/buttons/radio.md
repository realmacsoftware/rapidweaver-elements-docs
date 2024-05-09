# Radio

Radio Buttons can be used to show several buttons where only one button is active at a time. Selecting another button will deselect the currently active button. The property always contains the value from the active button. A format may be added to apply additional formatting on the value. Only one default should be set.

{% hint style="info" %}
**Important:** This documentation is incomplete and missing options.

Check back soon for a complete list.
{% endhint %}

### Supported Options <a href="#key-value-pairs-explained" id="key-value-pairs-explained"></a>

The radio buttons control supports the following options.

| Key             | Type   | Notes                                                                                                                                                                     |
| --------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `buttons`       | object | An object describing the type of buttons and available items.                                                                                                             |
| `buttons.items` | array  | An array of buttons to display. See the [Button Items option](radio.md#button-items-options) table below                                                                  |
| `buttons.style` | string | Should be set to `radio` to enable radio functionality.                                                                                                                   |
| `format`        | string | Can be used to apply additional formatting to the value. `{{value}}` will be replaced with the selected value. See [value formatting](../format.md) for more information. |
| `property`      | string | The name of the property set by this control.                                                                                                                             |
| `title`         | string | The name of the Slider. This will be displayed beside the UI element of RapidWeaver.                                                                                      |

### Button Items Options

| Key        | Type    | Notes                                                                                                                         |
| ---------- | ------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `default`  | boolean | Set to true if this is the default option. Should only be set on one item.                                                    |
| `icon`     | string  | Name of the icon to show on the button. Can be any icon from the [Font Awesome 4 library](https://fontawesome.com/v4/icons/). |
| `subtitle` | string  | A subtitle to display next to the button.                                                                                     |
| `value`    | string  | The value the button represents. The property will be set to this value when the button is active.                            |

### Radio Button Example

You can use the following code as a starting point for a radio button with four values.

```
{
    "title": "Align",
    "property": "textAlign",
    "format": "text-{{value}}",
    "buttons": {
        "style": "radio",
        "items": [{
            "subtitle": "Left",
            "value": "left",
            "icon": "fa-align-left",
            "default": true
        }, {
            "subtitle": "Center",
            "value": "center",
            "icon": "fa-align-center"
        }, {
            "subtitle": "Right",
            "value": "right",
            "icon": "fa-align-right"
        }, {
            "subtitle": "Justify",
            "value": "justify",
            "icon": "fa-align-justify"
        }]
    }
}
```

