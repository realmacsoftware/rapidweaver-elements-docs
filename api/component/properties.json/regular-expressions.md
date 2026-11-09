# Regular Expressions

RegEx (Regular Expression) is a powerful tool for searching, matching, and manipulating text based on specific patterns. It uses a combination of characters, meta-characters, and quantifiers to define complex search criteria. RegEx is widely used in programming, text editors, and command-line tools for tasks like input validation, pattern extraction, and string replacement. Its versatility allows users to efficiently find and process text, from simple matches to intricate parsing operations.

In Elements it can be used to conditionally check for values. The following example checks a coupon code format before showing a discount slider.

```json
{
  "groups": [{
    "title": "Coupon Settings",
    "properties": [{
      "title": "Coupon Code",
      "id": "couponCode",
      "text": {
        "default": "SAVE10",
        "subtitle": "Use SAVE10, SAVE20, etc."
      }
    }, {
      "visible": "couponCode matches /^SAVE[0-9]{2}$/",
      "title": "Discount",
      "id": "discountPercent",
      "format": "{{value}}%",
      "slider": {
        "default": 10,
        "min": 0,
        "max": 50,
        "round": true,
        "units": "%"
      }
    }]
  }]
}
```

{% embed url="https://share.cleanshot.com/fTrDTMb6" %}
