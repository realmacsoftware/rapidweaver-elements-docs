# Anchor

Setting an anchor in a template file will list it and allow it to be linked to from the Link Panel in the Editor.

```html
<div id="@anchor("myAnchor")"></div>
```

And using a property:

```html
<div id="@anchor(myAnchorProperty)"></div>
```

{% hint style="info" %}
See also [rw.addAnchor](../../hooks.js/available-functions/rw.addanchor.md) in the hooks file.
{% endhint %}

