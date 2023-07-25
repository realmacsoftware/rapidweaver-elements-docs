# Value Formatting

## Value Formatting

In some cases, it's adventagous to add additional formatting around a value before it's used in the templates. To achieve this, add a "format" property to the configuration specifying the format string.&#x20;

For example, the following creates a slider ranging from 0-12 with a property called `padding`

```
{
    "title" : "Padding",
    "property" : "padding",
    "default" : 5,
    "format": "pt-{{value}}",  
    "slider": {
        "min" : 0,
        "max" : 12
    }
}
```

If the slider is set to 5 and the template contains&#x20;

```
%id=padding%
```

&#x20;the output will be&#x20;

```
pt-5
```

