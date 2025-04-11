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

The Site Template has access to the following properties.

<table><thead><tr><th width="275">Property Name</th><th width="135">Type</th><th width="338">Description</th></tr></thead><tbody><tr><td><code>{{page.id}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.title}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.menuTitle}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.filename}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.ext}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.language}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.absolutePath}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.docRootPath}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.isFolder}}</code></td><td>Boolean</td><td>Does this page represent a folder</td></tr><tr><td><code>{{page.displayInMenu}}</code></td><td>Boolean</td><td>Should the page be shown in menus</td></tr><tr><td><code>{{page.isDraft}}</code></td><td>Boolean</td><td>Draft pages are not published</td></tr><tr><td><code>{{page.icon.url}}</code></td><td>String</td><td>Path to the page icon</td></tr></tbody></table>

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

### Dev Diary Videos for Site Templates

The following videos will show you how to use the Template feature in Elements. The videos were recorded with a development version of Elements so the feature(s) available now may differ slightly to those in the video.

{% embed url="https://www.youtube.com/watch?v=3_2D73Eg52Y" %}
