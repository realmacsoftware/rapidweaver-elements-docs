# Theme Spacing

Displays the Theme Studio Spacing control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Card Padding",
  "id": "cardPadding",
  "themeSpacing": {
    "mode": "padding",
    "default": {
      "base": {
        "left": "sm",
        "right": "sm",
        "top": "sm",
        "bottom": "sm"
      },
      "md": {
        "left": "lg",
        "right": "lg",
        "top": "lg",
        "bottom": "lg"
      }
    }
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Card Layout",
    "properties": [{
      "title": "Card Padding",
      "id": "cardPadding",
      "themeSpacing": {
        "mode": "padding",
        "default": {
          "base": {
            "left": "sm",
            "right": "sm",
            "top": "sm",
            "bottom": "sm"
          },
          "md": {
            "left": "lg",
            "right": "lg",
            "top": "lg",
            "bottom": "lg"
          }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

The `themeSpacing` attribute should be used for all space settings like padding, margins, gaps, translate, and positioning.

This control allows the user's site to dynamically adapt to any theme updates, changes, or overrides to the spacing scale.

The themeSpacing control has the following modes:

* padding
* margin
* gap
* transition
* position
* single

Each one of these modes correspond to the appropriate Tailwind utility classes. This means both developers and users can manage one single spacing scale that help promote consistency across all sites built in RapidWeaver Elements. See the examples below for more information.

```json
{
  "groups": [{
    "title": "Section Spacing",
    "properties": [{
      "title": "Section Padding",
      "id": "sectionPadding",
      "themeSpacing": {
        "mode": "padding",
        "default": {
          "base": {
            "left": "md",
            "right": "md",
            "top": "xl",
            "bottom": "xl"
          },
          "md": {
            "left": "2xl",
            "right": "2xl",
            "top": "2xl",
            "bottom": "2xl"
          }
        }
      }
    }]
  }]
}
```

### Single Mode

The single mode allows you to access the spacing scale from the Theme Studio in a single select control. This is handy when you need to set a single property rather than all four properties (top, right, bottom left). For example, if you need to set only the `top` css property you can do so like this:

```json
{
  "title": "Badge Offset",
  "id": "badgeOffsetTop",
  "format": "top-{{value}}",
  "themeSpacing": {
    "mode": "single",
    "default": {
      "base": {
        "value": "2"
      }
    }
  }
}
```

In this example, the default value will be returned as `top-2`.

### Custom Values

You can also specify that a custom value should be used by default for the themeSpacing control. This allows you to gain precise control over the value of the spacing when your element is dropped on to a page.

Set `custom` to `true` inside a breakpoint's default and the value is treated as an arbitrary CSS value instead of a step on the theme's spacing scale. Any CSS length or keyword can be used, such as `200px`, `100%`, `64`, or `auto`.

```json
{
  "title": "Sidebar Width",
  "id": "sidebarWidth",
  "format": "w-{{value}}",
  "themeSpacing": {
    "mode": "single",
    "default": {
      "base": {
        "custom": true,
        "value": "200px"
      }
    }
  }
}
```

Custom defaults also work per side in `padding` and `margin` modes:

```json
{
  "title": "Card Padding",
  "id": "cardPadding",
  "themeSpacing": {
    "mode": "padding",
    "default": {
      "base": {
        "custom": true,
        "left": 10,
        "right": 20,
        "top": 30,
        "bottom": 40
      }
    }
  }
}
```

When `custom` is `false` (or omitted), the values reference the theme's spacing scale (for example `sm`, `lg`, `2xl`) so they stay in sync with Theme Studio.

### Linking Values

In `padding` and `margin` modes the control displays link toggles that keep opposite sides in sync — when linked, editing one side also updates its partner. Use `linkHorizontal` (left/right) and `linkVertical` (top/bottom) inside a breakpoint's default to set the initial state of these toggles:

```json
{
  "title": "Section Padding",
  "id": "sectionPadding",
  "themeSpacing": {
    "mode": "padding",
    "default": {
      "base": {
        "left": "sm",
        "right": "sm",
        "top": "xl",
        "bottom": "xl",
        "linkHorizontal": true,
        "linkVertical": true
      }
    }
  }
}
```

### Supported Options

The themeSpacing control supports the following options.

| Key       | Type    | Notes                                                                                                                                                              |
| --------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `mode`    | string  | One of `padding`, `margin`, `gap`, `transition`, `position`, or `single`. Determines which Tailwind utility classes the control maps to.                            |
| `default` | object  | Per-breakpoint defaults (`base`, `sm`, `md`, …). Each breakpoint holds the four sides (`top`, `right`, `bottom`, `left`) or a single `value` when in `single` mode. |

Each breakpoint object inside `default` supports these keys:

| Key              | Type    | Notes                                                                                          |
| ---------------- | ------- | ---------------------------------------------------------------------------------------------- |
| `top` `right` `bottom` `left` | string | Spacing value per side (theme scale token, or an arbitrary CSS value when `custom` is `true`). |
| `value`          | string  | The single spacing value. Only used in `single` mode.                                          |
| `custom`         | boolean | When `true`, values are arbitrary CSS values instead of theme spacing tokens.                  |
| `linkHorizontal` | boolean | Links the left and right sides together.                                                       |
| `linkVertical`   | boolean | Links the top and bottom sides together.                                                       |

### Value

In templates, `{{id}}` outputs the Tailwind utility classes for the chosen mode, prefixed for each breakpoint the user has configured. In `single` mode the selected value is returned on its own, so combine it with [format](../general-structure/format.md) to build the class you need (for example `"format": "top-{{value}}"` returns `top-2`).
