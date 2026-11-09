---
description: Make component properties understandable to AI-assisted editing.
---

# AI

The `ai` key attaches metadata to a property that describes it to RapidWeaver Elements' AI-assisted editing. A well-described property lets the AI find and change the right setting when a user asks for something in plain language ("make the background a gradient", "align the label to the left").

The `ai` object sits alongside the control on a property, at the same level as `title` and `id`:

```json
{
  "title": "Alignment",
  "id": "align",
  "segmented": {
    "default": "center",
    "items": [
      { "value": "start", "icon": "arrow.left.to.line" },
      { "value": "center", "icon": "arrow.right.and.line.vertical.and.arrow.left" },
      { "value": "end", "icon": "arrow.right.to.line" }
    ]
  },
  "ai": {
    "name": "align",
    "description": "Label alignment within the button.",
    "values": ["start", "center", "end"]
  }
}
```

### Supported Options

| Key           | Type    | Notes                                                                                                                                          |
| ------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`        | string  | A short, stable name the AI uses to identify the property.                                                                                      |
| `description` | string  | What the property does, in plain language. Include the expected range or format where useful, e.g. `"Background color opacity, 0-100."`         |
| `values`      | array   | Optional list of allowed values, useful when the control's items don't make the valid options obvious.                                          |
| `visible`     | string  | Optional condition expression (same syntax as [visible](visible.md)) telling the AI when this property is relevant.                             |
| `exclude`     | boolean | Set to `true` to hide the property from AI-assisted editing entirely.                                                                           |

### Describing conditional properties

When a property only applies in certain configurations, mirror the relevant condition in `ai.visible` so the AI knows when the setting takes effect:

```json
{
  "title": "Gradient Direction",
  "id": "bgGradientDirection",
  "visible": "bg == 'static' && bgStyle == 'gradient'",
  "select": {
    "default": "bg-linear-to-r",
    "items": [
      { "value": "bg-linear-to-r", "title": "Left to Right" },
      { "value": "bg-linear-to-b", "title": "Top to Bottom" }
    ]
  },
  "ai": {
    "name": "bgGradientDirection",
    "description": "Linear gradient direction.",
    "visible": "bg == 'static' && bgStyle == 'gradient'"
  }
}
```

### Excluding properties

Use `exclude` for internal or duplicate properties that the AI shouldn't touch:

```json
"ai": {
  "name": "borderColor",
  "description": "Border theme color.",
  "exclude": true
}
```
