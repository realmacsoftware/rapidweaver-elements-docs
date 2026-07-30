---
description: Fully Customizable Site Template
icon: code
---

# Template

{% hint style="info" %}
The site template is **only used during preview and export**. It is not used in Edit mode.
{% endhint %}

The site template give you the ability to modify the underlying template code for your entire site. It's perfect for placing scripts, such as Google Analytics anywhere within the page structure.

The site template is used on every page of your website. If you need to insert a script just on specific pages, you should use the page level code areas instead.

<figure><img src="../../.gitbook/assets/CleanShot 2025-06-01 at 7 .11.12@2x.png" alt="Template Project Settings displaying the editable site HTML template"><figcaption></figcaption></figure>

### Properties

The Site Template has access to the following properties.

<table><thead><tr><th width="275">Property Name</th><th width="135">Type</th><th width="338">Description</th></tr></thead><tbody><tr><td><code>{{site.title}}</code></td><td>String</td><td>Website title</td></tr><tr><td><code>{{site.url}}</code></td><td>String</td><td>Website URL</td></tr><tr><td><code>{{page.title}}</code></td><td>String</td><td>Page title</td></tr><tr><td><code>{{page.path}}</code></td><td>String</td><td>Page path from site root</td></tr><tr><td><code>{{page.languageAttributes}}</code></td><td>String</td><td>Page language attributes</td></tr><tr><td><code>{{page.resourcesPath}}</code></td><td>String</td><td>Path to site resources directory</td></tr><tr><td><code>{{page.opengraph}}</code></td><td>String</td><td>OpenGraph social meta tag</td></tr><tr><td><code>{{page.social.title}}</code></td><td>String</td><td>Title for social media</td></tr><tr><td><code>{{page.social.description}}</code></td><td>String</td><td>Description for social media</td></tr><tr><td><code>{{page.social.url}}</code></td><td>String</td><td>Full page URL</td></tr><tr><td><code>{{page.social.image}}</code></td><td>String</td><td>Image for social media</td></tr><tr><td><code>{{page.content}}</code></td><td>String</td><td>Page content</td></tr><tr><td><code>{{page.componentHeader}}</code></td><td>String</td><td>Headers required by components</td></tr><tr><td><code>{{page.componentCSS}}</code></td><td>String</td><td>CSS required by components</td></tr><tr><td><code>{{page.componentJS}}</code></td><td>String</td><td>JS required by components</td></tr><tr><td><code>{{page.componentPageStart}}</code></td><td>String</td><td>Code required by components at start of page</td></tr><tr><td><code>{{page.componentPageEnd}}</code></td><td>String</td><td>Code required by components at end of page</td></tr><tr><td><code>{{page.componentHeadStart}}</code></td><td>String</td><td>Code required by components at start of headers</td></tr><tr><td><code>{{page.componentHeadEnd}}</code></td><td>String</td><td>Code required by components at end of headers</td></tr><tr><td><code>{{page.componentBodyStart}}</code></td><td>String</td><td>Code required by components at start of body</td></tr><tr><td><code>{{page.componentBodyEnd}}</code></td><td>String</td><td>Code required by components at end of body</td></tr><tr><td><code>{{page.customHeader}}</code></td><td>String</td><td>Custom page headers</td></tr><tr><td><code>{{page.customCSS}}</code></td><td>String</td><td>Custom page CSS</td></tr><tr><td><code>{{page.customJS}}</code></td><td>String</td><td>Custom page JS</td></tr><tr><td><code>{{page.customPageStart}}</code></td><td>String</td><td>Custom code at start of page</td></tr><tr><td><code>{{page.customPageEnd}}</code></td><td>String</td><td>Custom code at end of page</td></tr><tr><td><code>{{page.customHeadStart}}</code></td><td>String</td><td>Custom code at start of headers</td></tr><tr><td><code>{{page.customHeadEnd}}</code></td><td>String</td><td>Custom code at end of headers</td></tr><tr><td><code>{{page.customBodyStart}}</code></td><td>String</td><td>Custom code at start of body</td></tr><tr><td><code>{{page.customBodyEnd}}</code></td><td>String</td><td>Custom code at end of body</td></tr><tr><td><code>{{page.bodyClasses}}</code></td><td>String</td><td>required inside of classes body tag to support background colour</td></tr><tr><td><code>{{page.bodyAttributes}}</code></td><td>String</td><td>Should be placed inside of body tag to support custom attributes</td></tr></tbody></table>

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
<html class="scroll-smooth" {{page.languageAttributes}}>
<head>
    {{page.customHeadStart}}
    {{page.componentHeadStart}}
    
    <meta charset="utf-8">
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
<body class="{{page.bodyClasses}}" {{page.bodyAttributes}}>
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

### Example of adding Twitter/X social tags

You might like to add Twitter/X specific meta tags to your site so pages display correctly on their platform. Simply add the following to your site template.

```
    <!-- Twitter/X Card Tags (Ensures Proper Display on Twitter) -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="{{page.social.title}}">
    <meta name="twitter:description" content="{{page.social.description}}">
    <meta name="twitter:image" content="{{page.social.image}}">
    <meta name="twitter:url" content="{{page.social.url}}">
```

### Dev Diary Videos for Site Templates

The following videos will show you how to use the Template feature in Elements. The videos were recorded with a development version of Elements so the feature(s) available now may differ slightly to those in the video.

{% embed url="https://www.youtube.com/watch?v=3_2D73Eg52Y" %}
