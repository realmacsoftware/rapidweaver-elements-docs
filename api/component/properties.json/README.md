---
icon: sliders-simple
---

# Properties

Component properties (User Interface controls) are defined in the `properties.json` file. [Browse the UI Control docs](ui-controls/) for a full list of available controls and code samples.

An example `properties.json` file that creates a single group named "Hero Layout" with a few real-world controls.

```json
{
  "groups": [{
    "title": "Hero Layout",
    "icon": "rectangle.3.offgrid",
    "properties": [{
      "title": "Headline",
      "id": "heroHeadline",
      "text": {
        "default": "Build faster with Elements"
      }
    }, {
      "title": "Background Image",
      "id": "heroImage",
      "resource": {}
    }, {
      "title": "Overlay Opacity",
      "id": "overlayOpacity",
      "format": "bg-opacity-[{{value}}%]",
      "slider": {
        "default": 60,
        "min": 0,
        "max": 100,
        "units": "%",
        "round": true
      }
    }]
  }]
}

```
