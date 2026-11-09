---
description: Enable and disable controls based on another control's value.
---

# Enable

The `enable` key in an object's properties can be set using a logical expression that evaluates to `true` or `false`. This determines whether a specific UI element is enabled or disabled based on the conditions specified in the expression. Works in the same way as [visible](visible.md).

* **Boolean Logic**: Use logical operators (`&&`, `||`) to combine multiple conditions.
* **Comparison Operators**: Use `==`, `!=`, `>`, `<`, `>=`, `<=` to compare values.

## Examples

1.  **Complex Condition**

    ```json
    "enable": "(buttonStyle == 'filled' || buttonStyle == 'outline') && showIcon == true"
    ```

    This makes the control enabled only when a button style is chosen and icons are enabled.
2.  **Enabled Based on Numeric Ranges**

    ```json
    "enable": "imageBlur > 0 && imageBlur <= 20"
    ```

    Useful for enabling fine-tuning controls only when blur is active.
3.  **Negation to Disable**

    ```json
    "enable": "useCustomColors != true"
    ```

    The property is enabled when `useCustomColors` is `false`.

## Disabled

The `disabled` key is the inverse shorthand: instead of an expression, it takes an object with an `id` and a `value`. The control is disabled whenever the referenced property equals the given value.

```json
{
  "title": "Text Shadow",
  "id": "textShadow",
  "disabled": {
    "id": "bgType",
    "value": "image"
  },
  "themeShadow": {
    "mode": "text",
    "default": {
      "name": "none"
    }
  }
}
```

In this example the Text Shadow control is greyed out while the `bgType` property is set to `image`.
