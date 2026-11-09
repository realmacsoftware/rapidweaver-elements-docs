---
description: Reusable value definitions for controls
---

# Properties

Use these in your controls with `"use": "Name"` to get pre-defined option lists.

| use | Description | Default |
|-----|-------------|---------|
| `BackgroundType` | [View details](background-type.md) | - |
| `ButtonSize` | [View details](button-size.md) | `md` |
| `ContainerWidths` | [View details](container-widths.md) | `full` |
| `ContainerHeights` | [View details](container-heights.md) | `full` |
| `FontWeight` | [View details](font-weight.md) | `400` |
| `GradientDirection` | [View details](gradient-direction.md) | `bg-gradient-to-b` |
| `LetterSpacing` | [View details](letter-spacing.md) | `normal` |
| `LineHeight` | [View details](line-height.md) | `normal` |
| `RevealAnimations` | [View details](reveal-animations.md) | `fade` |
| `Slider` | [View details](slider.md) | - |
| `TextAlign` | [View details](text-align.md) | `text-left` |
| `TransformOrigins` | [View details](transform-origins.md) | `center` |
| `TransitionNames` | [View details](transition-names.md) | `dim` |

## Usage

```json
{
  "title": "Weight",
  "id": "fontWeight",
  "select": {
    "use": "FontWeight"
  }
}
```

The property's `items` and `default` will be merged into your control definition.
