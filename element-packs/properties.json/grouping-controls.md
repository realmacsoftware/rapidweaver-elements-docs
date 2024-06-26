# Group

Groups allow you to organise similar settings into relevant groups.

{% hint style="info" %}
the **Icon** property uses SF Symbols. Please refer to the [SF Symbol app](https://developer.apple.com/sf-symbols/) for a list of available icons.
{% endhint %}

Here is an example emtpy group:

```
{
	"groups": [
			{
	  "title": "Untitled",
	  "icon": "paintpalette",
	  "properties": [
		  
		]
	}]
}
```

Controls should placed inside of the properties array. The following example has a heading and an image drop well inside of the group.

```
{
    "groups": [
        {
            "title": "Button Design",
            "icon": "paintpalette",
            "properties": [
                {
                    "title": "Title",
                    "property": "buttonTitle",
                    "default": "",
                    "inputs": {
                        "items": [
                            {
                                "property": "buttonText",
                                "default": ""
                            }
                        ]
                    }
                },
                {
                    "title": "Image",
                    "property": "buttonImage",
                    "image": {
                        
                    }
                },
                
            ]
        }
    ]
}
```