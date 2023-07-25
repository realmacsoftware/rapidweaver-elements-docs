# Radio Buttons

Radio Buttons can be used to show several buttons where only one button is active at a time. Selecting another button will deselect the currently active button. The property always contains the value from the active button. A format may be added to apply additional formatting on the value. Only one default should be set.

Example radio button configuration

```
{
    "buttons": {
    "style": "radio",
    "items": [
        {
        "subtitle": "Left",
        "value": "left",
        "icon": "fa-align-left",
        "default": true
        },
        {
        "subtitle": "Center",
        "value": "center",
        "icon": "fa-align-center"
        },
        {
        "subtitle": "Right",
        "value": "right",
        "icon": "fa-align-right"
        },
        {
        "subtitle": "Justify",
        "value": "justify",
        "icon": "fa-align-justify"
        }
    ]
    },
    "format": "text-{{value}}",
    "title": "Align2",
    "property": "textAlign2"
},
```

