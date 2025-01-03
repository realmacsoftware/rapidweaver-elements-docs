# Responsive Values

### Responsive Values

By default, Elements makes all property controls responsive, allowing users to override any control setting across different devices. Elements accomplishes this by appending Tailwind’s responsive modifiers to the control’s value. Let’s explore how this works in an example.

#### Responsive Example

In this example, a control uses Tailwind’s text transform utility classes. The user can customize the control’s value across devices by clicking the responsive icon (dot) next to the control title in Elements.

Initially, the `headingTextTransform` output is set to normal-case. However, once the user customizes this setting in Elements, it may look something like this: `normal-case sm:uppercase md:lowercase lg:capitalize`.

Elements automatically applies and manages these responsive modifiers, saving you the effort of manually setting values for each device size and applying the appropriate modifier.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Case",
    "id": "headingTextTransform",
    "select": {
        "default": "normal-case",
        "items": [
            {
                "value": "normal-case",
                "title": "None"
            },
            {
                "value": "uppercase",
                "title": "Uppercase"
            },
            {
                "value": "lowercase",
                "title": "Lowercase"
            },
            {
                "value": "capitalize",
                "title": "Capitalize"
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

### Multi Value Responsive

This even works for controls that require multiple classes as the value. So given the following control:

```
{
  "title": "Position",
  "id": "position",
   "select": {
     "default": "bottom-0 left-0",
     "items": [
       {
         "title": "Top Right",
         "value": "top-0 left-auto right-0"
       },
       {
         "title": "Bottom Left",
         "value": "bottom-0 left-0 right-auto"
       }
     ]
   }
}
```

You can expect the output of `position` to be `bottom-0 left-0 right-auto md:top-0 md:left-auto md: right-0`

### Disable Responsive Controls

To disable responsive values for your control, simply add `"responsive": false` to your control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Not Responsive",
    "id": "nonResponsiveControl",
    "responsive": false,
    "switch": {}
}
```
{% endtab %}
{% endtabs %}
