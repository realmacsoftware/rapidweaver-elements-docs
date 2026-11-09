# Information

Display some informational static text. The message comes from the property's `title` — the control itself takes no options, stores no value, and needs no `id`.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "information": {},
  "title": "Tip: Use short, action-oriented labels for buttons."
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Button Settings",
    "properties": [{
      "information": {},
      "title": "Tip: Use short, action-oriented labels for buttons."
    }, {
      "title": "Button Label",
      "id": "buttonLabel",
      "text": {
        "default": "Get Started"
      }
    }]
  }]
}
```
{% endtab %}
{% endtabs %}
