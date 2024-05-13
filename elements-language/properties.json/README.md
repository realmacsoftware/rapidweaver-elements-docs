# Properties.json

The properties.json file defines the User Interface for an Element. [Browse the UI Control docs](ui-controls/) for a full list of available controls.

```
{
    "groups": [{
        "title" : "Formatting",
        "icon": "textformat.size",
        "properties" : [{
            "title": "Alignment",
            "property": "alignment",
            "segmented": {
                "items": [{
                    "value": "align-left",
                    "icon": "text.alignleft"
                }, {
                    "value": "align-center",
                    "icon": "text.aligncenter",
                    "default": true
                }, {
                    "value": "align-right",
                    "icon": "text.alignright",
                    "title": "Right"
                }]
            }
        }]
    }]
}
```

An example of setting Default Properites on various controls.

```
{
    "groups": [{
        "title" : "Content",
        "properties" : [{
            "title": "Text Style",
            "property": "textStyle",
            "themeTextStyle": {
                "default": { "base":{"name": "lg"}, "sm":{"name":"2xl"}, "md":{"name":"4xl"} }
            }
        },{
            "title": "Theme Font",
            "property": "textFont",
            "themeFont": {
                "default": { "base": { "name": "heading" }, "sm": { "name": "quote" } }
            }
        }, {
            "title" : "Padding",
            "property" : "themeSpacing",
            "themeSpacing": {
                "mode": "padding",
                "default": {
                    "base": {
                        "custom": true,
                        "left" : 10,
                        "right" : 20,
                        "top" : 30,
                        "bottom" : 40,
                        "linkVertical": true
                    },
                    "sm": {
                        "custom": false,
                        "left" : "xl",
                        "right" : "xl",
                        "top" : "xl",
                        "bottom" : "xl",
                    }
                }
            }
        }, {
            "title": "Border Width",
            "property": "borderWidth",
            "themeBorderWidth": {
                "default": {
                    "base": {
                        "custom": false,
                        "left" : "2",
                        "right" : "2",
                        "top" : "2",
                        "bottom" : "2",
                        "linkHorizontal": true
                    },
                    "sm": {
                        "custom": false,
                        "left" : "8",
                        "right" : "8",
                        "top" : "8",
                        "bottom" : "8",
                        "linkHorizontal": true
                    },
                }
            }
        }, {
            "title": "Border Radius",
            "property": "borderRadius",
            "themeBorderRadius": {
                "default": {
                    "base": {
                        "custom": false,
                        "topLeft" : "sm", 
                        "topRight" : "sm",
                        "bottomLeft" : "sm",
                        "bottomRight" : "sm",
                        "linkHorizontal": true
                    },
                    "sm": {
                        "custom": true,
                        "topLeft" : 5,
                        "topRight" : 5,
                        "bottomLeft" : 5,
                        "bottomRight" : 5,
                        "linkHorizontal": true
                    },
                }
            }
        }, {
            "title": "Spacing",
            "property": "spacing",
            "themeSpacing": {
                "default": {
                    "base": {
                        "custom": false,
                        "left" : "sm",
                        "right" : "sm",
                        "top" : "sm",
                        "bottom" : "sm",
                        "linkHorizontal": true
                    },
                    "sm": {
                        "custom": false,
                        "left" : "lg",
                        "right" : "lg",
                        "top" : "lg",
                        "bottom" : "lg",
                        "linkHorizontal": true
                    },
                }
            }
        }, {
            "title" : "Shadow",
            "property" : "themeShadow",
            "mode": "shadow",
            "themeShadow": {
                "default": { "base":{"name": "sm"}, "sm":{"name": "lg"}, "md":{"name":"xl"} }
            }
        }, {
            "title": "Slider",
            "property": "slider",
            "slider": {
                "default": "45"
                "min": 20,
                "max": 60,
                "round": true,
                "units": "vw"
            }
        }, {
            "title": "Slider 2",
            "property": "slider2",
            "slider": {
                "default": { "base" : 20, "sm" : 30, },
                "min": 20,
                "max": 60,
                "round": true,
                "units": "vw"
            }
        }, {
            "title": "Slider 3",
            "property": "slider3",
            "slider": {
                "default": "3",
                "content": [
                    {"title": "a", "value": "2"}, 
                    {"title": "b", "value": "3"}, 
                    {"title": "c", "value": "4"}
                ]
            }
        }, {
            "title": "Alignment",
            "property": "alignment",
            "segmented": {
                "default": {
                    "base": "w-auto",
                    "md": "w-full"
                },
                "items": [{
                    "value": "w-full",
                    "icon": "text.alignleft"
                }, {
                    "value": "w-asdf",
                    "icon": "text.alignleft"
                }, {
                    "value": "w-auto",
                    "icon": "text.aligncenter"
                }, {
                    "value": "custom",
                    "icon": "text.alignright",
                    "title": "Custom"
                }]  
            }
        }]
    }]
}

```



