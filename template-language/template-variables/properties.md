---
description: Access the users project settings
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

| Property Name                  | Type    | Description |
| ------------------------------ | ------- | ----------- |
| `{{project.siteURL}}`          | String  |             |
| `{{project.mode}}`             | String  |             |
| `{{project.title}}`            | String  |             |
| `{{project.slogan}}`           | String  |             |
| `{{project.copyright}}`        | String  |             |
| `{{project.email}}`            | String  |             |
| `{{project.contactText}}`      | String  |             |
| `{{project.enableSocialTags}}` | Boolean |             |
| `{{project.language}}`         | String  |             |
| `{{project.logo.url}}`         | String  |             |
| `{{project.logo.alt}}`         | String  |             |



| Property Name         | Type    | Scope |
| --------------------- | ------- | ----- |
| `{{title}}`           | String  | Page  |
| `{{icon}}`            | String  | Page  |
| `{{url}}`             | String  | Page  |
| `{{isActive}}`        | Boolean | Page  |
| `{{isExternalPage}}`  | Boolean | Page  |
| `{{hasChildren}}`     | Boolean | Page  |
| `{{pageDepth}}`       | Number  | Page  |
| `{{openInNewWindow}}` | Boolean | Page  |



