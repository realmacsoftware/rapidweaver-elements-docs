# Color

There's two types of colour picker, a native color well, and a Tailwinds spefic colour chooser that integrates with the Theme Studio in RapidWeaver Elements.

### Standard Color Picker (color)

The Color control displays the standard macOS color well.

```
{
	  "title" : "Colors",
	  "property" : "colors",
	  "colors" : {
		  "items" : [{
			  "subtitle" : "Quote",
			  "default" : "#616161",
			  "property" : "colors-one"
		  }, {
			  "subtitle" : "Citation",
			  "default" : "#BFBFBF",
			  "property" : "colors-two"
		  }]
	  }
  },
```

### Tailwinds Color Picker (customerColor)

We recommend this control be used when targeting the built-in Tailwinds framework.

```
{
	"title": "Color",
	"property": "customerColor",
	"default": "black",
	"format": "text-{{value}}",
	"themeColor": {}
  },
```

