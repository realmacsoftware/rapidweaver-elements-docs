---
description: Access Project Preties
---

# Properties

Various properties from the current environment can be used within templates but access must be granted through the `setProps` command in the hooks file first.

```
const transformHook = (rw) => {    
    // Make sure we have access to properties within the template
    rw.setProps({
        project: rw.project,
        page: rw.page,
        node: rw.node,
        element: rw.element
    })
}

exports.transformHook = transformHook;
```

With this in place, we gain access to the following within template files.

### Project Properties

<table><thead><tr><th width="346">Property Name</th><th width="127">Type</th><th width="278">Description</th></tr></thead><tbody><tr><td><code>{{project.siteURL}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.mode}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.title}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.slogan}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.copyright}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.email}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.contactText}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.enableSocialTags}}</code></td><td>Boolean</td><td></td></tr><tr><td><code>{{project.language}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.logo.url}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.logo.alt}}</code></td><td>String</td><td></td></tr></tbody></table>

### Page Properties

<table><thead><tr><th width="241">Property Name</th><th width="237">Type</th><th width="100">Description</th></tr></thead><tbody><tr><td><code>{{page.title}}</code></td><td></td><td></td></tr><tr><td><code>{{page.id}}</code></td><td></td><td></td></tr><tr><td><code>{{page.language}}</code></td><td></td><td></td></tr><tr><td><code>{{page.filename}}</code></td><td></td><td></td></tr><tr><td><code>{{page.ext}}</code></td><td></td><td></td></tr><tr><td><code>{{page.absolutePath}}</code></td><td></td><td></td></tr><tr><td><code>{{page.docRootPath}}</code></td><td></td><td></td></tr></tbody></table>



<table><thead><tr><th width="241">Property Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><code>{{icon}}</code></td><td></td><td></td></tr><tr><td><code>{{url}}</code></td><td></td><td></td></tr><tr><td><code>{{isActive}}</code></td><td></td><td></td></tr><tr><td><code>{{isExternalPage}}</code></td><td></td><td></td></tr><tr><td><code>{{hasChildren}}</code></td><td></td><td></td></tr><tr><td><code>{{pageDepth}}</code></td><td></td><td></td></tr><tr><td><code>{{openInNewWindow}}</code></td><td></td><td></td></tr></tbody></table>
