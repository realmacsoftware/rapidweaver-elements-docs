# Theme Color

Displays the Theme Studio Color control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Button Color",
  "id": "buttonColor",
  "format": "bg-{{value}}",
  "themeColor": {
    "default": {
      "name": "brand",
      "brightness": 500
    }
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Button",
    "properties": [{
      "title": "Button Color",
      "id": "buttonColor",
      "format": "bg-{{value}}",
      "themeColor": {
        "default": {
          "name": "brand",
          "brightness": 500
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

For consistency and integration with the Theme Studio in RapidWeaver Elements, use the `themeColor` attribute to specify all color options for your elements. This ensures that the color settings are centrally managed and adaptable to theme changes.

**Usage of `themeColor`:**

* **default**: Sets the initial or fallback color and brightness. In this case, the default color is brand with a brightness value of 500.

**Output Example:** [The `format` key](../general-structure/format.md) controls the output format of the `buttonColor` property. In your template files, referencing `{{buttonColor}}` with the example configuration above would output: `bg-brand-500`.

### Setting Light and Dark mode colours

```json
"themeColor": {
  "default": {
    "name": "surface",
    "brightness": 800,
    "darkName": "surface",
    "darkBrightness": 50
  }
}
```

### Supported Options

The themeColor control supports the following options.

| Key       | Type   | Notes                                                                                                                              |
| --------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| `default` | object | The default color. Supports `name` and `brightness`, plus `darkName` and `darkBrightness` for a separate dark-mode color.            |
| `mode`    | string | Set to `"single"` to display a single color selection without the separate dark-mode variant.                                        |
| `hover`   | object | Use in place of `default` when the property controls a hover-state color. Same shape as `default` (`name`, `brightness`).            |

A hover-state color is typically paired with a `hover:` prefixed [format](../general-structure/format.md):

```json
{
  "title": "Color",
  "id": "menuItemHoverColor",
  "format": "hover:text-{{value}}",
  "themeColor": {
    "hover": {
      "name": "brand",
      "brightness": 500
    }
  }
}
```

### Value

In templates, `{{id}}` returns the selected color token — the color name and brightness joined with a hyphen, for example `brand-500`. Combine it with [format](../general-structure/format.md) to build the utility class or CSS value you need.

### Using Tailwind 4 CSS Custom Properties

Tailwind 4 exposes every theme colour as a CSS custom property under the `--color-*` namespace (for example, `--color-brand-500`). This means the Theme Color control isn't limited to generating utility classes — you can format its value as a `var()` reference and use the selected colour directly in your CSS.

{% hint style="info" %}
This requires a theme with `tailwindVersion` set to `v4` in its `info.json`. See [What are Themes?](../../../theme/what-are-themes.md) for details.
{% endhint %}

Set the `format` to wrap the value in a `var()` reference:

```json
{
  "title": "Color 1",
  "id": "color1",
  "format": "var(--color-{{value}})",
  "themeColor": {
    "default": {
      "name": "brand",
      "brightness": 500
    }
  }
}
```

You can then use the property anywhere a CSS colour value is accepted, such as a [CSS template file](../../templates/css-templates.md):

```css
.color1 {
    color: {{color1}};
}
```

With the configuration above, the processed CSS would be:

```css
.color1 {
    color: var(--color-brand-500);
}
```

Because the colour is resolved by the browser through the CSS custom property, the output always stays in sync with the active theme — changing the colour in Theme Studio updates everywhere the variable is used.

This pattern is useful when a utility class can't reach the CSS property you need to style — for example gradient stops, borders on pseudo-elements, SVG fills, or values inside `@keyframes` — while still letting users pick colours from the standard Theme Studio palette.

It's also ideal for styling third-party libraries that require CSS overrides. Libraries such as sliders, lightboxes, and date pickers ship with their own class names (and often their own CSS custom properties) that you can't add Tailwind utility classes to. With a `var()` formatted Theme Color you can override the library's styles from a CSS template while keeping the colour choice in Theme Studio:

```css
/* Override a slider library's pagination colour */
.slider-{{id}} .slider-pagination-bullet-active {
    background: {{color1}};
}

/* Or reassign a custom property the library exposes */
.slider-{{id}} {
    --slider-theme-color: {{color1}};
}
```

