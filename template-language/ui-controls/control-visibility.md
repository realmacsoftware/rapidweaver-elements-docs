---
description: Show and hide controls based on another control's value.
---

# Visibility

You can modify the visibility of each control by checking the value of another control's value.

### Basic Example

```
{
  "groups": [
    {
      "title": "Spacing",
      "properties": [
        {
          "detail": {},
          "default": false,
          "property": "customSpacing"
        },
        {
          "visible": {
            "property": "customSizing",
            "value": true
          },
          "information": {},
          "title": "I am shown when customSizing is true"
        },
        {
          "visible": {
            "property": "customSizing",
            "value": false
          },
          "information": {},
          "title": "I am shown when customSizing is false"
        },
        ...
      ]
    }
  ]
}
```

### Example with operators

```
{
  "groups": [
    {
      "title": "Spacing",
      "properties": [
        {
          "visible": {
            "property": "exampleTextProperty",
            "operator: "!="
            "value": "hello world"
          },
          "information": {},
          "title": "Shown when the exampleTextProperty string is not equal to 'hello world'"
        },
        {
          "visible": {
            "property": "exampleTextProperty",
            "operator: "=="
            "value": "hello world"
          },
          "information": {},
          "title": "Shown when the exampleTextProperty string is equal to 'hello world'"
        },
        ...
      ]
    }
  ]
}
```

### Operators

<table><thead><tr><th width="240">Operator</th><th width="124.33333333333331">Type</th><th>Notes</th></tr></thead><tbody><tr><td>==</td><td>any</td><td></td></tr><tr><td>!=</td><td>any</td><td></td></tr><tr><td>&#x3C;</td><td>number</td><td></td></tr><tr><td>&#x3C;=</td><td>number</td><td></td></tr><tr><td>></td><td>number</td><td></td></tr><tr><td>>=</td><td>number</td><td></td></tr><tr><td>contains</td><td>string</td><td></td></tr><tr><td>matches</td><td>string</td><td></td></tr><tr><td>caseInsensitiveMatches</td><td>string</td><td></td></tr></tbody></table>
