# Theme Border Radius

Displays the Theme Studio Border Radius control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Card Radius",
  "id": "cardRadius",
  "themeBorderRadius": {
    "default": {
      "base": {
        "topRight": "lg",
        "topLeft": "lg",
        "bottomRight": "lg",
        "bottomLeft": "lg"
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
      "title": "Card Radius",
      "id": "cardRadius",
      "themeBorderRadius": {
        "default": {
          "base": {
            "topRight": "lg",
            "topLeft": "lg",
            "bottomRight": "lg",
            "bottomLeft": "lg"
          }
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

A single radius applied to all corners can be set with the `value` key instead of the four corner keys:

```json
{
  "title": "Radius",
  "id": "imageRadius",
  "themeBorderRadius": {
    "default": {
      "base": {
        "value": "lg"
      }
    }
  }
}
```

### Supported Options

The themeBorderRadius control supports the following options.

| Key       | Type   | Notes                                                                            |
| --------- | ------ | --------------------------------------------------------------------------------- |
| `default` | object | Per-breakpoint defaults (`base`, `sm`, `md`, …). See the breakpoint keys below.    |

Each breakpoint object inside `default` supports these keys:

| Key              | Type    | Notes                                                                                                  |
| ---------------- | ------- | -------------------------------------------------------------------------------------------------------- |
| `topLeft` `topRight` `bottomLeft` `bottomRight` | string | Radius per corner, as a theme border-radius token (for example `none`, `sm`, `lg`, `3xl`). |
| `value`          | string  | A single radius applied to all corners.                                                                   |
| `custom`         | boolean | When `true`, values are arbitrary CSS values instead of theme tokens.                                     |
| `linkHorizontal` | boolean | Sets the initial state of the link toggle that keeps corner values in sync.                               |

### Value

In templates, `{{id}}` outputs the Tailwind border-radius utility classes for the selected corners, prefixed for each breakpoint the user has configured.
