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
<a href="{{link.href}}" target="{{link.target}}>Click Me</a>
```
