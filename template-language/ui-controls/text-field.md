# Text Field

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



### Named Properties

If you would like the ability to reference an input directly you can add a `property` key like so:

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
                        "property" : "Name",
                        "default" : "Mario"
                    }, {
                        "property" : "Occupation",
                        "default" : "Plumber"
                    }]
                }
            }
      ],
    }]
}
```

This allows you to use `%id=Name%` and `%id=Occupation%` in your template files, rather than needing to referencing the index of your property.

#### Named Property Example

```
file: templates/each/index.html
---
<!-- With Named Properties -->
<h1>%id=Name%</h1>
<h2>%id=Occupation%</h2>

<!-- Without Named Properties -->
<h1>%id=MyTextField[0]%</h1>
<h2>%id=MyTextField[1]%</h2>
```
