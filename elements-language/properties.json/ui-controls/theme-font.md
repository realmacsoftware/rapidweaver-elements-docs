# Theme Font

For effective theme integration in RapidWeaver Elements, it is recommended to use the `themeFont` attribute to define all font family settings for your elements. This approach ensures that font preferences are coordinated with the overall theme settings, providing a consistent user experience.

Here’s a structured example for defining a font property:

```json
{
    "groups": [{
        "title": "TextArea Example",
        "properties": [{
            "title": "Theme Font",
            "property": "fontFamily",
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

**Output Example:** In your template files, referencing `{{fontFamily}}` with the example configuration above would output: `font-sub-heading sm:font-heading md:font-quote`.
