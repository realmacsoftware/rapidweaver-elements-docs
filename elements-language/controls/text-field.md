# Text Fields

A text field can be used for freeform text input.

{% hint style="info" %}
**Important:** This documentation is incomplete and missing options.

Check back soon for a complete list.
{% endhint %}



### Text Field

The following code exampledisplay a single text field.

```
{
    "groups": [        
      {
        "title" : "Section Title",
        "properties" : [
            {
                "title": "Text Fields",
                "property": "MyTextField",
                "inputs" : {
                    "items" : [{
                        "subtitle" : "one",
                        "default" : "a"
                    }]
                }
            }
      ],
    }]
    
}
```

The following code example displays an array of text fields.

```
{
    "groups": [        
      {
        "title" : "Section Title",
        "properties" : [
            {
                "title": "Text Fields",
                "property": "MyTextField",
                "inputs" : {
                    "items" : [{
                        "subtitle" : "one",
                        "default" : "a"
                    }, {
                        "subtitle" : "two",
                        "default" : "b"
                    }, {
                        "subtitle" : "three",
                        "default" : "c"
                    }]
                }
            }
      ],
    }]
    
}
```

### Multi-line Text Field

The following code example displays a multi-line text box.

```
{
    "groups": [        
      {
        "title" : "Section Title",
        "properties" : [
            {
                "multi": {},
                "title":"Text",
                "property" : "text",
                "default" : "my default text"
            }
      ],
    }]
    
}
```



