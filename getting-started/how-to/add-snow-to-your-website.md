---
description: During the winter you might want to add snow to your website…
---

# Add Snow to Your Website

Adding a snow effect can bring some festive character to your website. This tutorial shows you how to create a lightweight snow animation using JavaScript in Elements.

{% embed url="https://youtu.be/eI6RlZaKuu8?si=VwooSVpKzTlfkZ0Q" %}

### Element Project File

The completed project file is included below for your convenience.

* [Open Snow Demo in Elements](elementsapp://downloadDocument/J4j0QV3JuqJR)

### Resources:

Links to the resources used int he Tutorial:

* Snowstorm JS Script by Scott Schiller: [https://www.schillmania.com/projects/snowstorm/](https://www.schillmania.com/projects/snowstorm/)
* CDN JS: [https://cdnjs.com/libraries/Snowstorm](https://cdnjs.com/libraries/Snowstorm)

### Custom Component Code

To create the Custom Component shown in the tutorial, copy and paste the following code into the Template and Properties areas in Elements.

Place the following code in your **Template:**

```html
@portal(headEnd)
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Snowstorm/20131208/snowstorm.js" integrity="sha512-N8H1tAcm2/wJx02Q3FznOerQj4sFIdQJpmntt0/7ufMLh8dH1DFf7Zss+lbL7JwtYJuGVV+cVmWOdTA4x2lOTg==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <script>
        snowStorm.flakesMaxActive = {{snowAmount}};
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

