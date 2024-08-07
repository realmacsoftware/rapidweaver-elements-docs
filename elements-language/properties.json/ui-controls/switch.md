# Switch

The following examples returns a true or false value.

```
{
          "title": "Visible",
          "property": "display",
          "switch": {
            "trueValue": true,
            "falseValue": false,
            "default": true
          }
        },  
```

In the Template file you can do the following to display different html based on the value.

```
@if(display)
    <div class="p-sm text-lg text-center text-primary-500">I'm True!</div>
@else
    <div class="p-sm text-lg text-center text-primary-500">I'm False!</div>
@endif
```

The following example returns a string value.

```
{
          "title": "Visible",
          "property": "display",
          "switch": {
            "trueValue": "Hello",
            "falseValue": "Goodbye",
            "default": true
          }
        },
```

To display this value in the template file you can call the property name of `{{display}}`.
