# Visible

The `visible` key in an object's properties can be set using a logical expression that evaluates to `true` or `false`. This determines whether a specific UI element is shown or hidden based on the conditions specified in the expression. Works in the same way as [enabled](enabled.md).

* **Boolean Logic**: Use logical operators (`&&`, `||`) to combine multiple conditions.
* **Comparison Operators**: Use `==`, `!=`, `>`, `<`, `>=`, `<=` to compare values.

## Examples

1.  **Complex Condition**

    ```json
    "visible": "(backgroundType == 'custom' || backgroundType == 'image') && textColor == 'white'"
    ```

    This makes the property visible only if the backgroundType is either custom' or 'image', and the textColor is 'white'.
2.  **Visibility Based on Numeric Ranges**

    ```json
    "visible": "opacity > 20 && opacity < 30"
    ```

    Useful for showing elements that should only be visible within a specific range, e.g., showing a message if the opacity is not between 20-30.
3.  **Negation to Hide Elements**

    ```json
    "visible": "mySwitchControl != true"
    ```

    The property is visible when `mySwitchControl` is `false`.

The following example code toggles the visibility of controls based on the value of the switch.

```
{
    "groups": [{
        "title": "SWITCH TEST",
        "icon": "switch.2",
        "properties": [{
            "title": "Test Switch",
            "property": "testSwitch",
            "responsive": false,
            "switch": {
                "default": false
            }
        }, {
            "information": {},
            "title": "No Controls",
            "visible": "testSwitch == false"
        }, {
            "information": {},
            "title": "Let's Slide…",
            "visible": "testSwitch == true"
        }, {
            "title": "slider",
            "property": "slider",
            "visible": "testSwitch != true",
            "slider": {
                "default": 5,
                "min": 1,
                "max": 50,
                "round": true
            }
        }]
    }]
}
```
