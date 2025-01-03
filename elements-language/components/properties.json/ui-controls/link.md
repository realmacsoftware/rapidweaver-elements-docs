# Link

The Link control allows users to input a URL or link to another page within their RapidWeaver project.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Link",
    "id": "link",
    "link": {
        "subtitle": "Link to another page"
    }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "Link Example",
        "properties": [{
            "title": "Link",
            "id": "link",
            "link": {
                "subtitle": "Link to another page"
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}

### Template Example

The following will give you access to the link object in your template file(s).

```html
<a href="{{link.href}}" target="{{link.target}}">Click Me</a>
```

### Getting the Absolute URL

By default the link attribute will return a relative URL. To get the full URL add the absoluteURL property.

```json
        {
          "title": "Link",
          "id": "globalLink",
          "link": {
            "absoluteURL": true
          }
        }
```

Corresponding template example using the absoluteURL.

```html
<a href="{{redirectURL.href}}">Click Me</a>
```

