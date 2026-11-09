---
description: Using CSS files in the templates directory with template directives
---

# CSS Templates

CSS files placed in the `templates/` directory are processed through the Elements template engine, allowing you to use property insertion, conditionals, and other template directives within your stylesheets. This enables dynamic, component-specific styling based on user properties.

## Overview

CSS template files provide:

* **Property insertion** - Use component properties in CSS values
* **Conditional styles** - Include or exclude CSS based on conditions
* **Dynamic selectors** - Generate class names from properties
* **Per-instance processing** - Each component instance gets its own processed CSS

{% hint style="info" %}
In the core components, most production styling is done with Tailwind utility classes generated in `hooks.js` and inserted into HTML with `{{classes.*}}` — see [Component Styling](../component-styling.md). Template CSS files are used sparingly — mostly small editor-focused helpers, often gated by `@if(edit)` (see the [Tabs example](#tabs-component-edit-mode-styles) below).
{% endhint %}

## File Location

```
com.yourcompany.component/
├── templates/
│   ├── index.html
│   ├── styles.css         # Component styles
│   └── include/
│       └── ...
```

Any `.css` file at the root of `templates/` is processed — the filename is up to you. The core components use names like `styles.css` (Reveal), `edit.css` (Grid), and `editor-ui.css` (Tabs, Container, Shapes).

## Basic Usage

CSS files can use standard CSS syntax along with Elements template directives:

```css
.component-{{id}} {
    background-color: {{backgroundColor}};
    padding: {{spacing}}px;
}

@if(showBorder)
.component-{{id}} {
    border: {{borderWidth}}px solid {{borderColor}};
    border-radius: {{borderRadius}}px;
}
@endif
```

## Property Insertion

Insert component properties directly into CSS values:

```css
/* Using color properties */
.header {
    color: {{textColor}};
    background: {{bgColor}};
}

/* Using numeric properties */
.container {
    max-width: {{maxWidth}}px;
    padding: {{paddingTop}}px {{paddingRight}}px {{paddingBottom}}px {{paddingLeft}}px;
}

/* Using string properties */
.element {
    font-family: {{fontFamily}};
    transition-duration: {{duration}}s;
}
```

## Conditional Styles

Use `@if` directives to conditionally include CSS rules. Template `@if` accepts a single condition only — compute comparisons in `hooks.js` first, then test the resulting boolean. See [Combining Conditions](../language/if.md#combining-conditions).

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { variant } = rw.props;
    rw.setProps({
        variantIsPrimary: variant === "primary",
        variantIsSecondary: variant === "secondary",
    });
};
```

```css
/* Show different styles based on a property */
@if(variantIsPrimary)
.button {
    background: blue;
    color: white;
}
@elseif(variantIsSecondary)
.button {
    background: gray;
    color: white;
}
@else
.button {
    background: transparent;
    color: blue;
}
@endif
```

## Component ID Scoping

Use the unique component `{{id}}` to scope styles to specific instances:

```css
/* Each component instance gets unique styles */
.gallery-{{id}} {
    grid-template-columns: repeat({{columns}}, 1fr);
    gap: {{gap}}px;
}

.gallery-{{id}} .item {
    aspect-ratio: {{aspectRatio}};
}
```

This is particularly useful when multiple instances of the same component exist on a page with different property values.

## Examples from Core Components

### Reveal Component (Dynamic Groups)

The Reveal component uses property insertion for dynamic group styling:

```css
.group\/{{id}}:has(>[data-rwx-droparea]) {
  max-width: 100%;
}

.group\/{{id}}:not(:has(>[data-rwx-droparea])) {
  max-width: unset;
}
```

This creates group selectors scoped to each component instance.

### Tabs Component (Edit-Mode Styles)

Several core CSS templates are small edit-mode helpers gated by `@if(edit)`. The Tabs component's `templates/editor-ui.css` hides every tab panel except the one being edited:

```css
@if (edit)

/* Tab panels in editor - show the one being edited */
[role="tabpanel"] {
    display: none;
}

/* The active panel should be visible */
[role="tabpanel"][data-tab-panel="{{editorActiveTabIndex}}"] {
    display: block;
}

@endif
```

`editorActiveTabIndex` is computed in `hooks.js` from the tab currently selected in the editor. Because the whole file is wrapped in `@if(edit)`, it produces no output at all on the published site.

### Responsive Styles

Generate responsive styles based on properties:

```css
@if(responsiveEnabled)
@media (max-width: 768px) {
    .component-{{id}} {
        flex-direction: column;
        padding: {{mobilePadding}}px;
    }
}
@endif

@media (min-width: 769px) {
    .component-{{id}} {
        flex-direction: row;
        padding: {{desktopPadding}}px;
    }
}
```

## Processing Behavior

### Per-Instance Processing

CSS template files are processed **once per component instance**. If you have three instances with different properties, you'll get three sets of CSS rules:

```css
/* Instance 1 with blue background */
.card-abc123 {
    background: blue;
}

/* Instance 2 with red background */
.card-def456 {
    background: red;
}

/* Instance 3 with green background */
.card-ghi789 {
    background: green;
}
```

### Inline Styles

The processed CSS is inserted inline into the page within `<style>` tags, not as external stylesheets.

## Templates vs Assets

Choose the right location for your CSS:

### Use `templates/` CSS When:

* Styles depend on component properties
* Styles need conditional logic
* Styles are instance-specific
* You need dynamic selectors or values

**Example:**

```css
.component-{{id}} {
    color: {{userSelectedColor}};
    font-size: {{fontSize}}px;
}
```

### Use `assets/` CSS When:

* Styles are static and don't change
* Styles are shared across all instances
* You want better caching and performance
* Styles are large frameworks or libraries

**Example:**

```css
/* Static base styles */
.component-base {
    display: flex;
    align-items: center;
}
```

### Combining Both

A common pattern is to use both:

```
components/
├── assets/
│   └── base.css          # Static styles for all instances
└── templates/
    └── dynamic.css       # Property-based styles per instance
```

## Best Practices

### Scope with Component ID

Always scope your CSS to prevent conflicts:

```css
/* Good - scoped to this instance */
.component-{{id}} .header {
    color: {{headerColor}};
}

/* Risky - could conflict with other components */
.header {
    color: {{headerColor}};
}
```

### Keep Templates CSS Minimal

Only include CSS that actually needs property insertion:

```css
/* Good - needs property value */
.component-{{id}} {
    background: {{bgColor}};
}

/* Better in assets/ - static value */
.component-{{id}} {
    display: flex;
    align-items: center;
}
```

### Use CSS Custom Properties

For complex styling systems, consider using CSS custom properties:

```css
.component-{{id}} {
    --primary-color: {{primaryColor}};
    --spacing: {{spacing}}px;
    --border-radius: {{borderRadius}}px;
}

.component-{{id}} .header {
    color: var(--primary-color);
    padding: var(--spacing);
    border-radius: var(--border-radius);
}
```

This keeps the template processing minimal while allowing CSS to handle the styling logic.

### Avoid Heavy Computation

Don't use template CSS for complex calculations. Do that in `hooks.js`:

```javascript
// hooks.js
const transformHook = (rw) => {
    const calculatedWidth = rw.props.baseWidth * rw.props.multiplier;
    rw.setProps({
        computedWidth: calculatedWidth
    });
};
exports.transformHook = transformHook;
```

```css
/* templates/styles.css */
.component-{{id}} {
    width: {{computedWidth}}px;
}
```

### Consider Performance

Remember that each component instance generates CSS. For components that might appear many times:

```css
/* This works but generates a lot of CSS for 50 instances */
.item-{{id}} {
    background: {{itemColor}};
}

/* Consider using inline styles in HTML instead */
```

In your HTML template:

```html
<div class="item" style="background: {{itemColor}}">
```

## Limitations

### No @import

CSS `@import` statements won't work in template CSS files as they're processed as inline styles:

```css
/* This won't work */
@import url('external-styles.css');

/* Put imports in assets/ instead */
```

### Limited Preprocessor Support

Template CSS files don't support Sass, Less, or other preprocessors. Use the Elements template language for logic instead.

### Browser Compatibility

Generated CSS still needs to be valid CSS. Template directives don't add vendor prefixes or polyfills:

```css
/* You still need to handle browser compatibility */
.component {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
}
```

## Common Patterns

### Theme Integration

There is no hooks API for reading theme colors — [`rw.theme`](../hooks.js/available-data/rw.theme.md) exposes breakpoints, not colors. Core components apply theme colors with Tailwind utility classes instead: a [Theme Color control](../properties.json/ui-controls/theme-color.md) with `format: "bg-{{value}}"` delivers a ready-made class such as `bg-brand-500`, which `hooks.js` merges into the component's class strings:

```javascript
// hooks.js
const transformHook = (rw) => {
    const { backgroundColor } = rw.props; // already formatted, e.g. "bg-brand-500"

    const classes = {
        container: ["p-4", "rounded-lg", backgroundColor].join(" "),
    };

    rw.setProps({ classes });
};
exports.transformHook = transformHook;
```

If you need a theme color **inside** a CSS template (gradient stops, SVG fills), Tailwind 4 themes expose every theme color as a `--color-*` CSS custom property — format a Theme Color control as `var(--color-{{value}})` and interpolate that. See [Component Styling](../component-styling.md) for the full approach.

### Utility Classes

Generate utility classes based on properties:

```css
@if(showUtilities)
.text-{{customColorName}} {
    color: {{customColor}};
}

.bg-{{customColorName}} {
    background-color: {{customColor}};
}
@endif
```

### Animation Properties

Dynamic animations based on user settings. Compute the animation booleans in `hooks.js` first:

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { animation } = rw.props;
    rw.setProps({
        animationIsFade: animation === "fade",
        animationIsSlide: animation === "slide",
    });
};
```

```css
.component-{{id}} .animated {
    animation-duration: {{duration}}s;
    animation-timing-function: {{easing}};
    animation-delay: {{delay}}s;
}

@if(animationIsFade)
.component-{{id}} .animated {
    animation-name: fadeIn;
}
@elseif(animationIsSlide)
.component-{{id}} .animated {
    animation-name: slideIn;
}
@endif
```

## Related Documentation

* [Elements Language](../language/) - Template syntax reference
* [Templates Overview](./) - Understanding templates
* [Assets](../assets.md) - Static CSS files
* [Hooks.js](../hooks.js/) - Computing values for CSS
* [Properties](../properties.json/) - Defining CSS properties
