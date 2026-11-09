# Switch

Displays a switch, similar to a checkbox in functionality.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Show Icon",
  "id": "showIcon",
  "responsive": false,
  "switch": {
    "default": true
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
      "title": "Show Icon",
      "id": "showIcon",
      "responsive": false,
      "switch": {
        "default": true
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

The following example returns a true or false value. Note that `responsive` should be `false`.

```json
{
  "groups": [{
    "title": "Content",
    "properties": [{
      "title": "Show Badge",
      "id": "showBadge",
      "responsive": false,
      "switch": {
        "default": false
      }
    }]
  }]
}
```

The following example returns a string value instead of true or false. Note that `responsive` should be `false`.

```json
{
  "groups": [{
    "title": "Pricing",
    "properties": [{
      "title": "Price Label",
      "id": "priceLabel",
      "responsive": false,
      "switch": {
        "trueValue": "From $99",
        "falseValue": "From $129",
        "default": true
      }
    }]
  }]
}
```

To display this value in a template file, use `{{priceLabel}}`.

### Responsive

When using a switch responsively, trueValue and falseValue should be set to a Tailwind class name. You'll then receive a list of Tailwind classes within your template, prefixed for each breakpoint as necessary.

```json
{
  "groups": [{
    "title": "Layout",
    "properties": [{
      "title": "Show Description",
      "id": "showDescription",
      "responsive": true,
      "switch": {
        "trueValue": "block",
        "falseValue": "hidden",
        "default": {
          "base": false,
          "md": true
        }
      }
    }]
  }]
}
```

### Template

In the Template file you can do the following to display different html based on the value.

```html
@if(showDescription)
    <div class="p-sm text-lg text-center text-primary-500">I'm True!</div>
@else
    <div class="p-sm text-lg text-center text-primary-500">I'm False!</div>
@endif
```

### Supported Options

The switch control supports the following options.

| Key          | Type    | Notes                                                                                                        |
| ------------ | ------- | ------------------------------------------------------------------------------------------------------------ |
| `default`    | boolean | The default state of the switch. An object of per-breakpoint booleans when `responsive` is `true`.            |
| `trueValue`  | string  | The value returned when the switch is on. Use a Tailwind class when the control is responsive.                |
| `falseValue` | string  | The value returned when the switch is off. Use a Tailwind class when the control is responsive.               |
| `subtitle`   | string  | Helper text displayed underneath the switch.                                                                  |

### Value

The returned value depends on the configuration:

| Configuration                           | Return Value                                              |
| --------------------------------------- | --------------------------------------------------------- |
| `responsive: false`, no true/false values | `true` or `false`                                        |
| `responsive: false`, with true/false values | The `trueValue` or `falseValue` string                  |
| `responsive: true`, with true/false values | Tailwind classes prefixed per breakpoint, e.g. `hidden md:block` |
