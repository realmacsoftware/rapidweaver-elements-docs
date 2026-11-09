# Visible

The `visible` key in an object's properties can be set using a logical expression that evaluates to `true` or `false`. This determines whether a specific UI element is shown or hidden based on the conditions specified in the expression. Works in the same way as [enabled](enabled.md).

* **Boolean Logic**: Use logical operators (`&&`, `||`) to combine multiple conditions.
* **Comparison Operators**: Use `==`, `!=`, `>`, `<`, `>=`, `<=` to compare values.
* **Regex Match**: Use `matches` to perform a regex comparison.

## Examples

1.  **Complex Condition**

    ```json
    "visible": "(heroStyle == 'image' || heroStyle == 'video') && showOverlay == true"
    ```

    This makes the property visible only when a hero background is set and the overlay is enabled.
2.  **Visibility Based on Numeric Ranges**

    ```json
    "visible": "overlayOpacity > 20 && overlayOpacity < 80"
    ```

    Useful for showing fine-tuning controls only when the opacity is in a middle range.
3.  **Negation to Hide Elements**

    ```json
    "visible": "showBadge != true"
    ```

    The property is visible when `showBadge` is `false`.
4.  **Match a regex**

    ```json
    "visible": "couponCode matches /^SAVE[0-9]{2}$/"
    ```

    The property is visible when `couponCode` looks like `SAVE10` or `SAVE25`.

The following example toggles visibility based on a switch and a regex match.

```json
{
  "groups": [{
    "title": "CTA Badge",
    "icon": "tag",
    "properties": [{
      "title": "Show Badge",
      "id": "showBadge",
      "responsive": false,
      "switch": {
        "default": false
      }
    }, {
      "title": "Badge Text",
      "id": "badgeText",
      "visible": "showBadge == true",
      "text": {
        "default": "Limited Offer"
      }
    }, {
      "title": "Badge Offset",
      "id": "badgeOffset",
      "visible": "showBadge == true",
      "slider": {
        "default": 8,
        "min": 0,
        "max": 24,
        "round": true,
        "units": "px"
      }
    }]
  }, {
    "title": "Coupon Rules",
    "icon": "ticket",
    "properties": [{
      "title": "Coupon Code",
      "id": "couponCode",
      "responsive": false,
      "text": {}
    }, {
      "information": {},
      "title": "Valid format: SAVE10, SAVE25",
      "visible": "couponCode matches /^SAVE[0-9]{2}$/"
    }]
  }]
}
```
