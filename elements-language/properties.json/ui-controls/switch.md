# Switch

The following examples returns a true or false value. Note that `responsive` should be `false`.

```
{
    "groups": [{
        "title": "Switch Example",
        "properties": [{
            "title": "Visible",
            "property": "display",
            "responsive": false,
            "switch": {
                "default": true
            }
        }]
    }]
}
```

In the Template file you can do the following to display different html based on the value.

```
@if(display)
    <div class="p-sm text-lg text-center text-primary-500">I'm True!</div>
@else
    <div class="p-sm text-lg text-center text-primary-500">I'm False!</div>
@endif
```

The following example returns a string value instead of true or false. Note that `responsive` should be `false`.

```
{
    "groups": [{
        "title": "Switch Example",
        "properties": [{
            "title": "Prices Inc VAT",
            "property": "includeVATMessage",
            "responsive": false,
            "switch": {
                "trueValue": "Price includes VAT",
                "falseValue": "Price does not include VAT",
                "default": true
            }
        }]
    }]
}
```

To display this value in a template file, use `{{display}}`.



### Responsive

When using a switch responsively, trueValue and falseValue should be set to a Tailwind class name. You'll then receive a list of Tailwind classes within your template, prefixed for each breakpoint as necessary.

```
{
    "groups": [{
        "title": "Responsive Switch Example",
        "properties": [{
            "title": "Show Detail",
            "property": "showDetail",
            "responsive": true,
            "switch": {
                "trueValue": "block",
                "falseValue": "hidden",
                "default": {
                    "base": false,
                    "md": true,
                }
            }
        }]
    }]
}
```
