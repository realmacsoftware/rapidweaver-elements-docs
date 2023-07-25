# Slider

A slider can be used for choosing from a range of values.

{% hint style="info" %}
**Important:** This documentation is incomplete and missing options.

Check back soon for a complete list.
{% endhint %}

### Supported Options <a href="#key-value-pairs-explained" id="key-value-pairs-explained"></a>

The slider control supports the following options.

#### title

**`Key:`**`title`\
**`Type:`**`string`

The name of the Slider. This will be displayed beside the UI element of RapidWeaver.

#### content

**`Key:`**`content`\
**`Type:`**`array`

Can be used to specify an array of values to the slider. See [code example](slider.md#slider-example) below.



### Slider Example

You can use the following code as a starting point for a stepped slider with seven values.

```
{
    "title": "Contrast",
    "property": "contrast",
    "default": "contrast-70",
    "slider": {
        "content": [
            { "value": "contrast-0", "title": "0" },
            { "value": "contrast-50", "title": "50" },
            { "value": "contrast-70", "title": "75" },
            { "value": "contrast-100", "title": "100" },
            { "value": "contrast-125", "title": "125" },
            { "value": "contrast-150", "title": "150" },
            { "value": "contrast-200", "title": "200" }
        ]
    }
},
```

