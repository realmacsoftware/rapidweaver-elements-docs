# Format

In some cases, it's adventagous to format a value before it's passed to your element's templates. To achieve this, add a `format` property to the configuration specifying the format string.

**Value formatting is support by all controls.**

### Basic Example

For example, the following creates a slider ranging from 0-12 with a property called `padding`

```
{
    "title" : "Padding",
    "property" : "padding",
    "format": "pt-{{value}}",  
    "slider": {
        "default" : 5,
        "min" : 0,
        "max" : 12
    }
}
```

If the slider is set to 5 and the template contains&#x20;

```
{{padding}}
```

&#x20;the output will be&#x20;

```
pt-5
```

### Arbitrary Value Example

You could also format the control's value to use tailwind's arbitrary value feature. This would allow your element precis control over all css properties. For example, you can control the opacity utility class from tailwind with a slider:

```
{
    "title" : "Opacity",
    "property" : "opacity",
    "format": "opacity-[{{value}}%]",  
    "slider": {
        "default" : 50,
        "min" : 0,
        "max" : 100
    }
}
```

If the slider is set to 50 and the template contains&#x20;

```
{{opacity}}
```

&#x20;the output will be&#x20;

```
opacity-[50%]
```

### Advanced CSS Example

You could also format the control's value to output a valid CSS property. For example, if we want to control the translateX css property with a number input, we can do the following:

```
{
    "title" : "Translate X",
    "property" : "translateX",
    "format": "transform: translateX({{value}}px);",  
    "number": {
        "default" : 50,
    }
}
```

If the number field is set to 50 and the template contains&#x20;

```
{{translateX}}
```

&#x20;the output will be&#x20;

```
transform: translateX(50px);
```

Of cause, in this case you would want to add this to a CSS template file.

### CSS Custom Property Example

You can even use the format to control a CSS Custom Property (css variable). If we take our previous example and expand on it, we might want to instead set a `--translateX` CSS custom property with a number input:

```
{
    "title" : "Translate X",
    "property" : "translateX",
    "format": "--translateX: {{value}}px;",  
    "number": {
        "default" : 50,
    }
}
```

If the number field is set to 50 and the template contains&#x20;

```
{{translateX}}
```

&#x20;the output will be&#x20;

```
transform: translateX(50px);
```

In this case you would either want to add this to a CSS file, or use an inline style attribute to set the `--translateX`:

```
// first you would use the CSS custom property in your CSS:
<style>
.myDiv {
  ...
  transform: scale(0.5) translateX(var(--translateX, 0));
}

// now that your class is setup to use the --translateX custom property
// you can reassign it locally:
<div class="myDiv" style="{{translateX}}"> ... </div>

// this would output:
<div class="myDiv" style="--translateX: 50px;"> ... </div>
```
