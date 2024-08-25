# Theme Font

Displays the Theme Studio Font control.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Theme Font",
    "id": "fontFamily",
    "themeFont": {
        "default": {
            "base": { "name": "body" },
            "sm": { "name": "heading" },
            "md": { "name": "quote" }
        }
    }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "Theme Font Example",
        "properties": [{
            "title": "Theme Font",
            "id": "fontFamily",
            "themeFont": {
                "default": {
                    "base": { "name": "body" },
                    "sm": { "name": "heading" },
                    "md": { "name": "quote" }
                }
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}

For effective theme integration in RapidWeaver Elements, it is recommended to use the `themeFont` attribute to define all font family settings for your elements. This approach ensures that font preferences are coordinated with the overall theme settings, providing a consistent user experience.

Here’s a structured example for defining a font property:

**Output Example:** In your template files, referencing `{{fontFamily}}` with the example configuration above would output: `font-sub-heading sm:font-heading md:font-quote`.
