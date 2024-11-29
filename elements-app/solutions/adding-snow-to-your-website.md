# Adding Snow to your Website

Adding a snow effect to your website is a fun way to bring festive cheer to your projects in December. It creates a cozy seasonal atmosphere, delights visitors, and adds personality to your design, making your site more memorable and shareable. In this tutorial, we’ll show you how to easily implement a lightweight snow animation using JavaScript in Elements, perfect for enhancing your holiday-themed websites.

{% embed url="https://youtu.be/eI6RlZaKuu8?si=VwooSVpKzTlfkZ0Q" %}

### Element Project File

The completed project file is included below for your convenience.

* [Open Snow Demo in Elements](elementsapp://downloadDocument/J4j0QV3JuqJR)

### Resources:

Links to the resources used int he Tutorial:

* Snowstorm JS Script by Scott Schiller: [https://www.schillmania.com/projects/snowstorm/](https://www.schillmania.com/projects/snowstorm/)
* CDN JS: [https://cdnjs.com/libraries/Snowstorm](https://cdnjs.com/libraries/Snowstorm)

### Custom Component Code

If you'd like to create the Custom Component show in the Tutorial, copy and paste the following code into the the Template Properties areas in Elements.

Place the following code in your **Template:**

```html
@portal(headEnd)
    <script src="resources/scripts/snowstorm.js"></script>
    <script>
        snowStorm.flakesMaxActive = {{snowAmount}};    // show more snow on screen at once
        snowStorm.followMouse = {{followMouse}};
    </script>
@endportal


```

Place the following code into the **Properties:**

```json
{
    "groups": [{
        "title": "Snow Settings",
        "properties": [{
            "title": "Amount",
            "id": "snowAmount",
            "format": "{{value}}",
            "slider": {
                "default": 50,
                "min": 0,
                "max": 512,
                "round": true
            }
        },
        {
    "title": "Follow Mouse",
    "id": "followMouse",
    "responsive": false,
    "switch": {
        "trueValue": "true",
        "falseValue": "false",
        "default": true
    }
}
        ]
    }]
}

```



