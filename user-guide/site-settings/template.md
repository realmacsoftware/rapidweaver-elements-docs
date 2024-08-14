---
description: Fully Customizable Site Template
---

# Template

{% hint style="info" %}
The site template is **only used during preview and export**. It is not used in Edit mode.
{% endhint %}

The site template give you the ability to modify the underlying template code for your entire site. It's perfect for placing scripts, such as Google Analytics anywhere within the page structure.&#x20;

The site template is used on every page of your website. If you need to insert a script just on specific pages, you should use the page level code areas instead.

### Page Properties

The Site Template has access to all the page level properties, such as `{{page.title}}` and `{{page.description}}`. A full list can be found in the [Available Data](../../elements-language/hooks.js/available-data/) section under [Page Properties](https://docs.realmacsoftware.com/elements-docs/elements-language/hooks.js/available-data#page-properties) in this manual.

To reference a file in you Resources folder you can use the following page tag to get the correct path to the resources folder:`{{page.resourcesPath}}.`

The following example shows how you might link to a "store.js" file that's in a "scripts" folder in the Resources area.

```
<script src="{{page.resourcesPath}}/scripts/javascript.js"></script>
```

### Site Template Example

The following is an example of the default site Template. Please note the template is only used during preview and export. It is not used in Edit mode.

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
