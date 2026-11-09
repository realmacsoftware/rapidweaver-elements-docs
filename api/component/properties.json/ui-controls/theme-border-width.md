# Theme Border Width

Displays the Theme Studio Border Width control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Card Border",
  "id": "cardBorderWidth",
  "themeBorderWidth": {
    "default": {
      "base": {
        "top": "1",
        "right": "1",
        "bottom": "1",
        "left": "1"
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
    "title": "Card Styles",
    "properties": [{
      "title": "Card Border",
      "id": "cardBorderWidth",
      "themeBorderWidth": {
        "default": {
          "base": {
            "top": "1",
            "right": "1",
            "bottom": "1",
            "left": "1"
          }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

The following example links all four sides together and starts with a 2 unit border:

```json
{
  "title": "Border",
  "id": "buttonBorderWidth",
  "themeBorderWidth": {
    "default": {
      "base": {
        "top": "2",
        "right": "2",
        "bottom": "2",
        "left": "2",
        "linkAll": true
      }
    }
  }
}
```

A named width from the theme can also be used as the default:

```json
{
  "title": "Border",
  "id": "cellBorderWidth",
  "themeBorderWidth": {
    "default": {
      "base": {
        "name": "none"
      }
    }
  }
}
```

### Supported Options

The themeBorderWidth control supports the following options.

| Key       | Type   | Notes                                                                            |
| --------- | ------ | --------------------------------------------------------------------------------- |
| `default` | object | Per-breakpoint defaults (`base`, `sm`, `md`, …). See the breakpoint keys below.    |

Each breakpoint object inside `default` supports these keys:

| Key              | Type    | Notes                                                                          |
| ---------------- | ------- | -------------------------------------------------------------------------------- |
| `top` `right` `bottom` `left` | string | Border width per side, as a theme border-width token.               |
| `name`           | string  | A named theme border width applied to all sides, for example `none`.             |
| `custom`         | boolean | When `true`, values are arbitrary CSS values instead of theme tokens.            |
| `linkHorizontal` | boolean | Links the left and right sides together.                                          |
| `linkVertical`   | boolean | Links the top and bottom sides together.                                          |
| `linkAll`        | boolean | Links all four sides together.                                                    |

### Value

In templates, `{{id}}` outputs the Tailwind border-width utility classes for the selected sides, prefixed for each breakpoint the user has configured.
