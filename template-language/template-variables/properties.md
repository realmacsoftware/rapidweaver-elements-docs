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



**Title**&#x20;

Plain text value.

```
%rw:projectTitle%
```

**Slogan**&#x20;

Plain text value.

```
%rw:projectSlogan%
```

**Footer**

Plain text value.

```
%rw:projectFooter%
```

**Email**

Plain text value.

```
%rw:projectEmail%
```

**Contact Text**

Plain text value.

```
%rw:projectContactText%
```

**Base URL**

Plain text value.

```
%rw:projectBaseURL%
```

**Enable Social Tags**

Bool, returns a string of "True" or "False".

```
%rw:projectEnableSocialTags%
```

**Twitter Account**

Plain text value.

```
%rw:projectTwitterAccount%
```

**Project Language**

Plain text value.

```
%rw:projectLanguage%
```

**Banner URL**

Plan text value.

```
%rw:projectBannerURL%
```

**Banner Alt Text**

Plan text value.

```
%rw:projectBannerAltText%
```

**Logo URL**

Plan text value.

```
%rw:projectLogoURL%
```

**Logo Alt Text**

Plan text value.

```
%rw:projectLogoAltText%
```

### Code Example

The following example outputs the project title and slogan along with a list of all supported properties.

```
<H1>%rw:projectTitle%</h1>
<h2>%rw:projectSlogan%</h2>

<ul>
  <li>
    <strong>projectFooter:</strong> %rw:projectFooter%
  </li>
  <li>
    <strong>projectEmail:</strong> %rw:projectEmail%
  </li>
  <li>
    <strong>projectContactText:</strong> %rw:projectContactText%
  </li>
  <li>
    <strong>projectBaseURL:</strong> %rw:projectBaseURL%
  </li>
  <li>
    <strong>projectEnableSocialTags:</strong> %rw:projectEnableSocialTags%
  </li>
  <li>
    <strong>projectTwitterAccount:</strong> %rw:projectTwitterAccount%
  </li>
  <li>
    <strong>projectLanguage:</strong> %rw:projectLanguage%
  </li>
  <li>
    <strong>projectBannerURL:</strong> %rw:projectBannerURL%
  </li>
  <li>
    <strong>projectBannerAltText:</strong> %rw:projectBannerAltText%
  </li>
  <li>
    <strong>projectLogoURL:</strong> %rw:projectLogoURL%
  </li>
  <li>
    <strong>projectLogoAltText:</strong> %rw:projectLogoAltText%
  </li>
</ul>
```

