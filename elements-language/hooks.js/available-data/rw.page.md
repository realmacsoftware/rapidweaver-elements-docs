# rw.page

The following template example will output the page (and folder) details for all the pages in a project.

<pre class="language-html"><code class="lang-html">@each(page in pages)
    {{page.title}}
    {{page.isPublished}}
    {{page.displayInMenu}}
    {{page.url}}
    {{page.isActive}}
<strong>    {{page.isExternalPage}}
</strong>    {{page.pageDepth}}
    {{page.openInNewWindow}}
    {{page.icon}}
    {{page.hasPages}}
    {{page.hasActiveChild}}

    @each(childpage in page.pages) 
<strong>        {{childpage.title}} 
</strong>    @endeach
@endeach
</code></pre>

Before you can access the page properties you'll need to include the following code in the Hooks.js

```javascript
const transformHook = (rw) => {    
    // Get pages from rw
    const pages = rw.pages
    
    // Set pages in our template data
    rw.setProps({ 
        pages
    })
}

exports.transformHook = transformHook;
```

