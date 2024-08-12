---
description: Site Template
---

# Template

{% hint style="info" %}
The site template is only used during preview and export. It is not used in Edit mode.
{% endhint %}

To reference a file in you Resources folder you can use the following tag to get the correct path to the resources folder:`{{page.resourcesPath}}.`

The following example shows how you might link to a "store.js" file in the Resources folder.

```
<script src="{{page.resourcesPath}}/scripts/javascript.js"></script>
```

Here's an example of the default site Template. Please note the template is only used during preview and export. It is not used in Edit mode.

```
{{page.customPageStart}}
{{page.componentPageStart}}

<!doctype html>
<html {{page.languageAttributes}}>
<head>
    {{page.customHeadStart}}
    {{page.componentHeadStart}}
    
    <meta http-equiv="x-ua-compatible" content="ie=edge">
    <meta name="viewport" content="width=device-width">
    {{page.componentHeader}}
    {{page.opengraph}}
    {{page.customHeader}}
    
    <title>{{page.title}}</title>
    
    {{page.componentCSS}}
    {{page.customCSS}}

    {{page.componentJS}}
    {{page.customJS}}

    {{page.componentHeadEnd}}
    {{page.customHeadEnd}}
</head>
<body>
    {{page.customBodyStart}}
    {{page.componentBodyStart}}

    {{page.content}}

    {{page.componentBodyEnd}}
    {{page.customBodyEnd}}
</body>
</html>

{{page.componentPageEnd}}
{{page.customPageEnd}}

```
