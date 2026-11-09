# Format

In some cases, it's advantageous to format a value before it's passed to your element's templates. To achieve this, add a `format` property to the configuration specifying the format string.

**Value formatting is supported by all controls.**

### Basic Example

For example, the following creates a slider ranging from 0-12 with a property called `cardPadding`.

```json
{
  "title": "Card Padding",
  "id": "cardPadding",
  "format": "p-{{value}}",
  "slider": {
    "default": 4,
    "min": 0,
    "max": 12
  }
}
```

If the slider is set to 5 and the template contains&#x20;

```text
{{cardPadding}}
```

&#x20;the output will be&#x20;

```text
p-4
```

### Arbitrary Value Example

You could also format the control's value to use Tailwind's arbitrary value feature. This would allow your element precise control over all CSS properties. For example, you can control the opacity utility class from Tailwind with a slider:

```json
{
  "title": "Overlay Opacity",
  "id": "overlayOpacity",
  "format": "opacity-[{{value}}%]",
  "slider": {
    "default": 70,
    "min": 0,
    "max": 100
  }
}
```

If the slider is set to 50 and the template contains&#x20;

```text
{{overlayOpacity}}
```

&#x20;the output will be&#x20;

```text
opacity-[70%]
```

### Advanced CSS Example

You could also format the control's value to output a valid CSS property. For example, if we want to control the translateX CSS property for an accent badge, we can do the following:

```json
{
  "title": "Badge Offset",
  "id": "badgeOffsetX",
  "format": "transform: translateX({{value}}px);",
  "number": {
    "default": 12
  }
}
```

If the number field is set to 50 and the template contains&#x20;

```text
{{badgeOffsetX}}
```

&#x20;the output will be&#x20;

```text
transform: translateX(12px);
```

Of course, in this case you would want to add this to a CSS template file.

### CSS Custom Property Example

You can even use the format to control a CSS Custom Property (CSS variable). If we take our previous example and expand on it, we might want to instead set a `--badgeOffsetX` CSS custom property with a number input:

```json
{
  "title": "Badge Offset",
  "id": "badgeOffsetX",
  "format": "--badgeOffsetX: {{value}}px;",
  "number": {
    "default": 12
  }
}
```

If the number field is set to 50 and the template contains&#x20;

```text
{{badgeOffsetX}}
```

&#x20;the output will be&#x20;

```text
--badgeOffsetX: 12px;
```

In this case you would either want to add this to a CSS file, or use an inline style attribute to set the `--translateX`:

```html
// first you would use the CSS custom property in your CSS:
<style>
.myDiv {
  ...
  transform: scale(0.5) translateX(var(--badgeOffsetX, 0));
}
</style>

// now that your class is setup to use the --badgeOffsetX custom property
// you can reassign it locally:
<div class="myDiv" style="{{badgeOffsetX}}"> ... </div>

// this would output:
<div class="myDiv" style="--badgeOffsetX: 12px;"> ... </div>
```
