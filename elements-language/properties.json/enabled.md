---
description: Show and hide controls based on another control's value.
---

# Enabled

The `enabled` key in an object's properties can be set using a logical expression that evaluates to `true` or `false`. This determines whether a specific UI element is enabled or disabled based on the conditions specified in the expression. Works in the same way as [visible](visible.md).

* **Boolean Logic**: Use logical operators (`&&`, `||`, `!`) to combine multiple conditions.
* **Comparison Operators**: Use `==`, `!=`, `>`, `<`, `>=`, `<=` to compare values.

## Examples

1.  **Complex Condition**

    ```json
    "enabled": "(backgroundType == 'custom' || backgroundType == 'image') && textColor == 'white'"
    ```

    This makes the property enabled only if the backgroundType is either custom' or 'image', and the textColor is 'white'.
2.  **Visibility Based on Numeric Ranges**

    ```json
    "enabled": "opacity > 20 && opacity < 30"
    ```

    Useful for enabling controls that should only be visible within a specific range.
3.  **Negation to Hide Elements**

    ```json
    "enabled": "!mySwitchControl"
    ```

    The property is enabled when `mySwitchControl` is `false`.
