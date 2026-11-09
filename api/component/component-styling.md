---
description: A standardized approach to building components with Tailwind CSS
icon: paintbrush
---

# Component Styling

Elements uses Tailwind CSS for all component styling. Following this approach ensures consistency across all components—whether built-in, third-party, or custom-made—and makes it easier for users to build sites that are cohesive and simple to update.

Elements compiles Tailwind for you: it scans your templates and the class strings your hooks generate, then builds the final stylesheet. There is no Tailwind config or build step inside a pack.

**Your main goal should always be to make a component that feels native to Elements.**

{% hint style="info" %}
The built-in components are Tailwind 4 ready, and every example on this page works with Tailwind 4. Themes declare the Tailwind version they use by setting `tailwindVersion` to `v4` in their `info.json`—see [What are Themes?](../theme/what-are-themes.md)
{% endhint %}

## Why Tailwind?

Tailwind offers a utility-first approach to styling. Instead of writing custom CSS, you apply small, reusable utility classes directly to your HTML elements. This approach provides several benefits:

- **Consistency**: All components share the same styling vocabulary
- **No style leakage**: Styles applied via utility classes stay within each component's HTML structure
- **Optimized output**: Elements generates only the CSS your page actually uses, resulting in smaller, more efficient stylesheets
- **Theme integration**: Utility classes map directly to Theme Studio values

## Theme-Driven Design

In Elements, styling configurations—colors, fonts, spacing, and more—are controlled by the Theme and managed through the Theme Studio. Components inherit styles from the theme rather than dictating their own.

This means:

- Users can switch themes without breaking their site's design
- All components "just work" within any project
- Styling remains consistent across the entire site

For example, a Heading component might define its default font family as `heading` and font size as `3xl`. The component doesn't care what specific font or pixel size these represent—it only needs to know the values exist. The Theme Studio handles the actual values, allowing full customization while maintaining compatibility.

## Theme UI Controls

When designing your component, use Theme-based UI Controls wherever possible. These controls integrate directly with the Theme Studio, ensuring your component respects the user's theme settings.

| Control | Purpose |
|---------|---------|
| [Theme Border Width](properties.json/ui-controls/theme-border-width.md) | Border thickness values |
| [Theme Border Radius](properties.json/ui-controls/theme-border-radius.md) | Corner rounding values |
| [Theme Color](properties.json/ui-controls/theme-color.md) | Color palette selection |
| [Theme Font](properties.json/ui-controls/theme-font.md) | Font family selection |
| [Theme Spacing](properties.json/ui-controls/theme-spacing.md) | Margin and padding values |
| [Theme Shadow](properties.json/ui-controls/theme-shadow.md) | Box shadow styles |
| [Theme Text Style](properties.json/ui-controls/theme-text-style.md) | Text size presets |
| [Theme Typography](properties.json/ui-controls/theme-typography.md) | Typography class selection |

## Theme Colors

All components need to work out of the box. Every Elements theme defines a set of semantic colors—use these rather than hard-coded palette colors so your component adapts to any theme:

| Color | Usage |
|-------|-------|
| `brand` | Dominant color for branding and key interactive items like buttons and links |
| `accent` | Complementary color for secondary elements and supporting details |
| `surface` | Background colors that provide contrast behind text and elements |
| `text` | Headings and body text |
| `black` / `white` | Pure black and pure white |

Each color comes in Tailwind's standard `50`–`950` brightness scale, and themes also include all of the default Tailwind color palettes. A [Theme Color](properties.json/ui-controls/theme-color.md) control resolves to a `name-brightness` token such as `surface-500`, ready to drop into a utility class. See [What are Themes?](../theme/what-are-themes.md) for the full list of tokens a theme provides.

## Applying Utilities Directly in Templates

For styling that doesn't need to be user-configurable, apply Tailwind utilities directly in your template files:

```html
<div class="flex items-center gap-4 p-6 bg-surface-50 rounded-lg shadow-md">
  <h2 class="text-xl font-heading text-text-900">{{title}}</h2>
  <p class="text-text-600">{{description}}</p>
</div>
```

This approach eliminates the need for scoped CSS—each component's styles are self-contained within its HTML structure.

## Generating Tailwind Classes with Format

Use the `format` key in your `properties.json` to transform property values into Tailwind utility classes. This keeps your templates clean and ensures proper class output.

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

In your template, reference the property directly:

```html
<button class="{{buttonColor}} px-4 py-2">Click Me</button>
```

This outputs:

```html
<button class="bg-brand-500 px-4 py-2">Click Me</button>
```

This is exactly how the built-in components work. The core Border Color control formats a Theme Color as a border utility:

```json
{
  "title": "Color",
  "id": "borderColor",
  "format": "border-{{value}}",
  "themeColor": {
    "default": {
      "name": "surface",
      "brightness": 500
    }
  }
}
```

`{{borderColor}}` outputs `border-surface-500`.

The same pattern works with any theme control. The core Button component uses a [Theme Spacing](properties.json/ui-controls/theme-spacing.md) control to set the gap between its icon and text:

```json
{
  "title": "Spacing",
  "id": "dropzoneSpacing",
  "format": "gap-x-{{value}}",
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

`{{dropzoneSpacing}}` outputs `gap-x-2`.

The `format` key works with any control type, including arbitrary values like `opacity-[{{value}}%]`. See [Format](properties.json/general-structure/format.md) for more examples.

## Responsive Styling

Elements supports responsive styling out of the box. Theme controls can define different values for each breakpoint using the standard Tailwind breakpoint prefixes.

```json
{
  "title": "Heading Size",
  "id": "headingSize",
  "themeTextStyle": {
    "default": {
      "base": { "name": "2xl" },
      "md": { "name": "3xl" },
      "lg": { "name": "4xl" }
    }
  }
}
```

This outputs responsive classes that apply at each breakpoint:

```html
<h1 class="text-2xl md:text-3xl lg:text-4xl">...</h1>
```

Supported breakpoints follow Tailwind's defaults:

| Prefix | Minimum Width |
|--------|---------------|
| `base` | 0px (default) |
| `sm` | 640px |
| `md` | 768px |
| `lg` | 1024px |
| `xl` | 1280px |
| `2xl` | 1536px |

## Composing Classes in hooks.js

Because formatted controls emit ready-made utility classes, most real components do their styling in [hooks.js](hooks.js/README.md): the hook gathers the class strings from `rw.props`, combines them with static classes and conditional logic, and applies the result to the component's root element. Templates stay clean because they never see the full class list.

Here's the pattern, simplified from the core Button component. It uses the `buttonColor` and `dropzoneSpacing` controls defined earlier on this page, and only plain JavaScript—paste it into a new project and it works:

```javascript
const transformHook = (rw) => {
    const { showText, dropzoneType, dropzoneSpacing, buttonColor } = rw.props;
    const { id } = rw.node;

    const wantsDropzone = dropzoneType != "false";

    const classes = [
        `group/button group/${id}`,
        "flex items-center cursor-pointer",
        "px-4 py-2 rounded-lg",
        buttonColor,
        wantsDropzone && dropzoneSpacing,
    ]
        .filter(Boolean)
        .join(" ");

    rw.setRootElement({
        as: "button",
        class: classes,
    });

    rw.setProps({
        wantsDropzone,
        dropzoneSide: dropzoneType == "right" ? "order-last" : "order-first",
        showText: showText == "true",
    });
};

exports.transformHook = transformHook;
```

A few things to notice:

- **Static classes** (`flex items-center cursor-pointer`) sit alongside **property-driven classes** (`buttonColor` is already `bg-brand-500` and `dropzoneSpacing` is already `gap-x-2`—formatted by their controls).
- **Conditional logic** decides which classes apply—`wantsDropzone && dropzoneSpacing` only includes the gap when the icon dropzone is enabled, and `.filter(Boolean)` drops any `false` or empty entries before joining.
- [`rw.setRootElement()`](hooks.js/available-functions/rw.setrootelement.md) applies the finished class string to the component's root element.
- Small presentational values pass to the template via [`rw.setProps()`](hooks.js/available-functions/rw.setprops.md).

The template only handles content and the few props it needs—this is the entire Button template:

```html
@if(showText)
@text("text", title: "Button Text", default: "Click Me")
@endif
@if(wantsDropzone)
<div class="{{dropzoneSide}}">
  @dropzone("dropzone", title: "Icon")
</div>
@endif
```

{% hint style="info" %}
The built-in components compose their classes exactly this way, but at a larger scale they use shared helpers—`classnames()`, `advancedClasses()`, and the `global*` family (`globalLayout`, `globalBorders`, and friends)—that ship with the [Build Tools](../development-resources/build-tools/README.md) and are bundled into `hooks.js` at build time. Plain arrays and `join(" ")` need no build step; reach for the Build Tools when your pack grows. See [classnames](../development-resources/build-tools/shared-hooks/core/classnames.md) and [globalBorders](../development-resources/build-tools/shared-hooks/borders/global-borders.md) for details.
{% endhint %}

### Combining Property Values

Hooks can merge multiple formatted controls into a single utility. The core border controls pair a Theme Color (`"format": "border-{{value}}"`) with an opacity slider (`"format": "[{{value}}%]"`), then join them with Tailwind's slash modifier:

```javascript
const borderClasses = borderColor
    .split(" ")
    .filter(Boolean)
    .map((c) => `${c.trim()}/${borderColorOpacity}`)
    .join(" ");
// → "border-surface-500/[100%]"
```

The `split`/`map` handles Theme Colors with separate light and dark values, which emit two space-separated classes (for example `border-surface-200 dark:border-surface-800`)—each one needs the opacity applied.

## Multi-Layer Components

More complex components style several elements, not just the root. The convention used throughout the core pack is to build a `classes` object in the hook—one class string per layer—and pass it to the template with `rw.setProps()`.

Simplified from the core Container component, which renders separate background and content layers stacked in a one-cell grid:

```javascript
const transformHook = (rw) => {
    const { spacingEnabled, margin, padding, contentGap, backgroundColor, borderRadius } = rw.props;
    const { id } = rw.node;

    const classes = {
        wrapper: [
            `group/container group/${id}`,
            "grid grid-cols-1 [&>*]:col-start-1 [&>*]:row-start-1 [&>*]:min-w-0",
            spacingEnabled == "true" && margin,
        ]
            .filter(Boolean)
            .join(" "),
        background: [
            "z-0 overflow-hidden",
            backgroundColor,
            borderRadius,
        ]
            .filter(Boolean)
            .join(" "),
        content: [
            "relative z-30 flex flex-col peer",
            contentGap,
            spacingEnabled == "true" && padding,
        ]
            .filter(Boolean)
            .join(" "),
    };

    rw.setRootElement({
        as: "div",
        class: classes.wrapper,
    });

    rw.setProps({ classes });
};

exports.transformHook = transformHook;
```

The template applies each layer's classes where they belong:

```html
<div class="{{classes.content}}">@dropzone("Content", title: "Container")</div>
<div class="{{classes.background}}"></div>
```

The wrapper is a one-cell grid, and `[&>*]:col-start-1 [&>*]:row-start-1` places every child in that same cell so the background, content, and any overlay stack on top of each other. Splitting the layers means borders, backgrounds, and effects can each target the right element independently.

## Advanced Tailwind Techniques

The core components lean on a handful of modern Tailwind features worth knowing about.

### Named Groups for Scoped Hover States

Every core component adds `group/${id}` to its root, where `id` is the component instance's unique identifier from `rw.node`. Child elements—or the hook's generated classes—can then use `group-hover/${id}:` variants that respond only to that instance:

```
group-hover/gGSPTx:border-brand-500/[100%]
```

Because the group name is unique per instance, hover states never leak between two copies of the same component on a page. The same idea works between sibling elements: the Container's content layer carries the `peer` class so the background layer can respond to it with `peer-hover:` variants. See [getHoverPrefix](../development-resources/build-tools/shared-hooks/core/get-hover-prefix.md) for the helper the core pack uses to pick the right variant.

### Arbitrary Variants

Arbitrary variants style descendants your template doesn't render directly. The core Text component applies user-chosen link styles to every `<a>` inside its rich text this way:

```javascript
const linkModifiers = [linkColor, linkUnderline, linkFontWeight]
    .map((value) => `[&_a]:${value}`)
    .join(" ");
// → "[&_a]:text-brand-500 [&_a]:underline [&_a]:font-medium"
```

The same technique handles pseudo-states on those descendants (`[&_a:hover]:`, `[&_a:visited]:`) and direct children (`[&>*]:`), as seen in the Container's grid stacking above.

### Data-Attribute Variants

State-dependent styling doesn't need JavaScript to toggle classes—use data-attribute variants and flip the attribute instead. The core border helper emits classes like:

```
data-[active=true]:border-brand-500/[100%]
```

The styles apply automatically whenever the element's `data-active` attribute is `"true"`.

### Dark Mode

A [Theme Color](properties.json/ui-controls/theme-color.md) control with `darkName`/`darkBrightness` set emits a pair of classes, for example `bg-surface-50 dark:bg-surface-800`. When a hook adds another variant on top of such a value, the new prefix must land *after* `dark:`—`[&_a]:text-brand-500 dark:[&_a]:text-brand-50`, not `[&_a]:dark:…`. The Build Tools include [injectPrefixOnDarkModeColors](../development-resources/build-tools/shared-hooks/core/inject-prefix-on-dark-mode-colors.md) to handle this rewrite for you.

## Supporting User-Defined Classes

Give power users an escape hatch. Every core component exposes an Advanced group in the inspector with a free-text CSS Classes control, and appends its value to the root class list:

```javascript
const advancedClasses = (rw) => {
    const { display, cssClasses, overflow, zIndex } = rw.props;

    return [display, cssClasses, overflow, zIndex].filter(Boolean).join(" ");
};
```

The [Build Tools](../development-resources/build-tools/README.md) ship a ready-made version of this helper—see [advancedClasses](../development-resources/build-tools/shared-hooks/core/advanced-classes.md).

Third-party components should follow the same convention so users can add their own utility classes to any component without editing templates.

---

## Custom CSS (When Necessary)

While Tailwind is the recommended approach, there are situations where custom CSS may be required. Use these techniques sparingly, as custom CSS will not be controllable from the Theme Studio.

### Using the Component ID for Scoping

You can scope CSS to a specific component instance using the `{{id}}` variable, which outputs a unique identifier for each component. CSS files placed in your component's `templates/` directory are processed through the template engine—see [CSS Templates](templates/css-templates.md) for full details.

**In your CSS template file:**

```css
.component-{{id}} {
  /* styles scoped to this component instance */
}

.component-{{id}} .child-element {
  /* styles for child elements */
}
```

**In your HTML template:**

```html
<div class="component-{{id}} ...">
  <span class="child-element">...</span>
</div>
```

### BEM Naming Convention

If you need multiple custom classes, use BEM (Block Element Modifier) naming with a unique prefix to avoid conflicts:

```css
.mycomponent-card {
  /* block styles */
}

.mycomponent-card__title {
  /* element styles */
}

.mycomponent-card--featured {
  /* modifier styles */
}
```

### CSS Custom Properties

For values that need to be dynamic, use CSS custom properties set via inline styles:

```json
{
  "title": "Animation Duration",
  "id": "animationDuration",
  "format": "--animation-duration: {{value}}ms;",
  "slider": {
    "default": 300,
    "min": 100,
    "max": 1000
  }
}
```

```html
<div class="animated-element" style="{{animationDuration}}">...</div>
```

```css
.animated-element {
  transition: transform var(--animation-duration, 300ms) ease;
}
```

This approach lets users control CSS values through the inspector while keeping the styling logic in CSS.

### Theme Colors in Custom CSS

With a Tailwind 4 theme (`tailwindVersion: "v4"`), every theme color is also exposed as a CSS custom property under the `--color-*` namespace. A Theme Color control formatted as `var(--color-{{value}})` can then be used directly in your CSS—ideal for gradient stops, SVG fills, or overriding third-party library styles while keeping the color choice in Theme Studio. See [Using Tailwind 4 CSS Custom Properties](properties.json/ui-controls/theme-color.md#using-tailwind-4-css-custom-properties).

## Related Documentation

* [Building Complex Components](../guides/README.md) - Guides applying these styling patterns in real components
* [Responsive Images & Media](../guides/responsive-images-and-media.md) - Breakpoint-keyed classes and dynamic CSS
* [Tutorial: Build an FAQ Component](../guides/tutorial/README.md) - Class composition applied step by step
