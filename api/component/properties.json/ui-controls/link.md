# Link

The Link control allows users to input a URL or link to another page within their RapidWeaver project.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "CTA Link",
  "id": "ctaLink",
  "link": {
    "subtitle": "Link to a product or signup page"
  }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "CTA Button",
    "properties": [{
      "title": "CTA Link",
      "id": "ctaLink",
      "link": {
        "subtitle": "Link to a product or signup page"
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
<a href="{{ctaLink.href}}" target="{{ctaLink.target}}">Get Started</a>
```

### Getting the Absolute URL

By default the link attribute will return a relative URL. To get the full URL add the absoluteURL property.

```json
{
  "title": "CTA Link",
  "id": "ctaLink",
  "link": {
    "absoluteURL": true
  }
}
```

Corresponding template example using the absoluteURL.

```html
<a href="{{ctaLink.href}}">Get Started</a>
```

### Supported Options

The link control supports the following options.

| Key           | Type    | Notes                                                                                     |
| ------------- | ------- | ------------------------------------------------------------------------------------------ |
| `default`     | object  | The default link. Supports the keys `href`, `text`, `target`, `title`, and `rel`.          |
| `subtitle`    | string  | Helper text displayed underneath the control.                                              |
| `absoluteURL` | boolean | When `true`, `href` returns the full URL instead of a relative one.                        |

```json
{
  "title": "Page Link",
  "id": "pageLink",
  "link": {
    "default": {
      "href": "",
      "text": "",
      "target": "_self",
      "title": "",
      "rel": ""
    }
  }
}
```

### Value

The control returns a link object. Access its properties in templates with dot notation — for example `{{pageLink.href}}` and `{{pageLink.target}}` as shown above.
