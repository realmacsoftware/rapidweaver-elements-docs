# Link

The Link control allows users to input a URL or link to another page within their RapidWeaver project.

### Properties.json

To add a Link to your Element's controls set the `"property"` to `"link"` in the properties.json file, like so:

```
{
  "title": "Link",
  "properties": [
    {
      "title": "Link",
      "property": "link",
      "link": {
        "subtitle": "Link to another page"
      }
    }
  ]
}
```

### Templates

This will give you access to the link object in your template files.

```
<a href="%id=link.href%" target="%id=link.target%>Click Me</a>
```
