---
description: Access Project Properties
---

# Available Data

Properties from the current environment can be used within templates but most of them need to be passed through using the `setProps` command in the [hooks.js](broken-reference) file first. The node object is always available.

```
const transformHook = (rw) => {    
    // Expose project, page and component objects to the template, node is always available
    rw.setProps({
        project: rw.project,
        page: rw.page,
        component: rw.component
    })
}

exports.transformHook = transformHook;
```

With this in place, we gain access to the following within template files.

### Project Properties

<table><thead><tr><th width="346">Property Name</th><th width="127">Type</th><th width="278">Description</th></tr></thead><tbody><tr><td><code>{{project.title}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.mode}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.siteURL}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.language}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.enableSocialTags}}</code></td><td>Boolean</td><td></td></tr><tr><td><code>{{project.allowDarkMode}}</code></td><td>Boolean</td><td></td></tr><tr><td><code>{{project.logo.url}}</code></td><td>String</td><td></td></tr><tr><td><code>{{project.logo.alt}}</code></td><td>String</td><td></td></tr></tbody></table>

### Page Properties

<table><thead><tr><th width="275">Property Name</th><th width="135">Type</th><th width="338">Description</th></tr></thead><tbody><tr><td><code>{{page.id}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.title}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.menuTitle}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.filename}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.ext}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.language}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.absolutePath}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.docRootPath}}</code></td><td>String</td><td></td></tr><tr><td><code>{{page.projectResourcesPath}}</code></td><td>String</td><td>Path to the project resources</td></tr><tr><td><code>{{page.isFolder}}</code></td><td>Boolean</td><td>Does this page represent a folder</td></tr><tr><td><code>{{page.displayInMenu}}</code></td><td>Boolean</td><td>Should the page be shown in menus</td></tr><tr><td><code>{{page.isDraft}}</code></td><td>Boolean</td><td>Draft pages are not published</td></tr><tr><td><code>{{page.icon.url}}</code></td><td>String</td><td>Path to the page icon</td></tr></tbody></table>

### Node Properties

The node object is always passed into templates and contains the following properties.

| Property Name               | Type   | Description                        |
| --------------------------- | ------ | ---------------------------------- |
| `{{node.id}}`               | String |                                    |
| `{{node.title}}`            | String |                                    |
| `{{node.parent.id}}`        | String |                                    |
| `{{node.parent.container}}` | String |                                    |
| `{{node.backendPath}}`      | String | Path to the node's backend folder. |

### Component Properties

<table><thead><tr><th width="249">Property Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><code>{{component.title}}</code></td><td>String</td><td></td></tr><tr><td><code>{{component.group}}</code></td><td>String</td><td></td></tr><tr><td><code>{{component.version}}</code></td><td>Integer</td><td></td></tr><tr><td><code>{{component.build}}</code></td><td>Integer</td><td></td></tr><tr><td><code>{{component.assetPath}}</code></td><td>String</td><td>Path to component assets</td></tr><tr><td><code>{{component.siteAssetPath}}</code></td><td>String</td><td>Path to component site assets</td></tr><tr><td><code>{{component.sharedAssetPath}}</code></td><td>String</td><td>Path to pack shared assets</td></tr></tbody></table>

