# Color

There's two types of colour picker, a native "[color well](../color.md)", and a Tailwinds specify colour picker that integrates with the Theme Studio in RapidWeaver Elements.

### Theme Studio Color Picker (themeColor)

We recommend this control be used when targeting the built-in Tailwinds framework.

```
{
	"title": "Color",
	"property": "customColor",
	"default": "black",
	"format": "text-{{value}}",
	"themeColor": {}
  },
```
