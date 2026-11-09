# Theme Shadow

Displays the Theme Studio Shadow control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Card Shadow",
  "id": "cardShadow",
  "themeShadow": {
    "default": {
      "name": "sm"
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
      "title": "Card Shadow",
      "id": "cardShadow",
      "themeShadow": {
        "default": {
          "name": "sm"
        }
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

### Modes

The `mode` option selects which kind of shadow the control manages:

```json
{
  "title": "Text Shadow",
  "id": "headingShadow",
  "themeShadow": {
    "mode": "text",
    "default": {
      "name": "none"
    }
  }
}
```

* `drop` — a drop shadow (`drop-shadow-*` utilities)
* `box` — a box shadow (`shadow-*` utilities)
* `text` — a text shadow

### Supported Options

The themeShadow control supports the following options.

| Key       | Type   | Notes                                                                                              |
| --------- | ------ | ---------------------------------------------------------------------------------------------------- |
| `mode`    | string | One of `drop`, `box`, or `text`.                                                                      |
| `default` | object | The default shadow as a `name` from the theme's shadow scale, e.g. `{ "name": "sm" }`. Can also be set per breakpoint: `{ "base": { "name": "sm" } }`. |

### Value

In templates, `{{id}}` outputs the utility classes for the selected theme shadow, prefixed for each breakpoint the user has configured.
