# Editable Content

The following tags should be placed in the html template file. Using any of the following tags enable editable areas with the page. No setup of configuration in the properties file is required.

### Editable Text

Add a simple editible text area with optional default text.

```
@text("heading")
```

An editable text area with a default value of "Hello World!".

```
@text("heading", default: "Hello World!")
```

### Editable Typography

Adds a text area that support the Typography feature.

```
 @richtext("heading", default: "Hello World!")
```

