# Radio Buttons

Radio Buttons can be used to show several buttons where only one button is active at a time. Selecting another button will deselect the currently active button. The property always contains the value from the active button. A format may be added to apply additional formatting on the value. Only one default should be set.

{% hint style="info" %}
**Important:** This documentation is incomplete and missing options.

Check back soon for a complete list.
{% endhint %}

### Supported Options <a href="#key-value-pairs-explained" id="key-value-pairs-explained"></a>

The radio buttons control supports the following options.

#### title

**`Key:`**`title`\
**`Type:`**`string`

The name of the Slider. This will be displayed beside the UI element of RapidWeaver.

#### property

**`Key:`**`property`\
**`Type:`**`string`

The name of the property

#### format

**`Key:`**`format`\
**`Type:`**`string`

Can be used to apply additional formatting to the value. `{{value}}` will be replaced with the selected value. See [code example](radio-buttons.md#radio-button-example) below.

#### buttons.style

**`Key:`**`style`\
**`Type:`**`string`

Should be set to `radio` to enable radio functionality.

#### buttons.items

**`Key:`**`items`\
**`Type:`**`array`

An array of buttons to display. Each button can be configured with the following options.

### Button Options <a href="#key-value-pairs-explained" id="key-value-pairs-explained"></a>

#### subtitle

**`Key:`**`subtitle`\
**`Type:`**`string`

A subtitle to display next to the button.

#### value

**`Key:`**`value`\
**`Type:`**`string`

The value the button represents. The property will be set to this value when the button is active.

#### icon

**`Key:`**`icon`\
**`Type:`**`string`

Name of the icon to show on the button. Can be any icon from the Font Awesome 4 library.

#### default

**`Key:`**`default`\
**`Type:`**`bool`

Set to true if this is the default option. Should only be set on one item.

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

