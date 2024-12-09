# Regular Expressions

RegEx (Regular Expression) is a powerful tool for searching, matching, and manipulating text based on specific patterns. It uses a combination of characters, meta-characters, and quantifiers to define complex search criteria. RegEx is widely used in programming, text editors, and command-line tools for tasks like input validation, pattern extraction, and string replacement. Its versatility allows users to efficiently find and process text, from simple matches to intricate parsing operations.

In Elements it can be used to conditionally check for values, the following example checks for specific words in a text field before showing a slider.

```json
{
    "groups": [{
        "title": "Text Field Example",
        "properties": [{
            "title": "Text Field",
            "property": "myText",
            "text": {
                "default" : "Hello World",
                "subtitle" : "two",
            }
        },{
        "visible": "myText matches /(this|that|other)+/",
        "title" : "vis",
        "property" : "slider",
        "default" : 21,
        "slider": {
            "min" : 0,
            "max" : 100,
            "round" : true
            } 
        }       
        ]
    }]
}
```

{% embed url="https://share.cleanshot.com/fTrDTMb6" %}
