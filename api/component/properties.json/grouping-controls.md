# Grouping Controls

Groups allow you to organise similar settings into relevant sections in the inspector.

{% hint style="info" %}
The **icon** property uses SF Symbols. Please refer to the [SF Symbol app](https://developer.apple.com/sf-symbols/) for a list of available icons.
{% endhint %}

Here is an example empty group:

```json
{
  "groups": [
    {
      "title": "Color Settings",
      "icon": "paintpalette",
      "properties": []
    }
  ]
}
```

### Group Icon

You can specify an icon to appear next to the title of your group. The **Icon** property uses SF Symbols. Please refer to the [SF Symbol app](https://developer.apple.com/sf-symbols/) for a list of available icons.

### Group Controls

Controls should be placed inside the properties array. The following example has a heading, a text field, and a resource dropwell inside the group.

```json
{
  "groups": [
    {
      "title": "Hero Content",
      "icon": "textformat.size",
      "properties": [
        {
          "title": "Headline",
          "id": "heroHeadline",
          "text": {
            "default": "Launch your next product"
          }
        },
        {
          "title": "Subheading",
          "id": "heroSubheading",
          "textArea": {
            "default": "A short sentence explaining the value proposition."
          }
        },
        {
          "title": "Background Image",
          "id": "heroImage",
          "resource": {}
        }
      ]
    }
  ]
}
```

The following example has two groups, one for content and one for media.

```json
{
  "groups": [{
    "title": "Content",
    "icon": "textformat",
    "properties": [{
      "title": "Title",
      "id": "cardTitle",
      "text": {
        "default": "Customer Story"
      }
    }]
  }, {
    "title": "Media",
    "icon": "photo",
    "properties": [{
      "title": "Image",
      "id": "cardImage",
      "resource": {}
    }]
  }]
}
```

### Conditional Groups

Groups support the same [visible](general-structure/visible.md) key as individual controls, so an entire section can be shown or hidden based on another property's value:

```json
{
  "groups": [{
    "title": "Footer Cells",
    "icon": "tablecells",
    "visible": "showFooter == true",
    "properties": [{
      "title": "Footer Text",
      "id": "footerText",
      "text": {
        "default": ""
      }
    }]
  }]
}
```

