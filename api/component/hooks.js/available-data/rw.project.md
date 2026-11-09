# rw.project

The `rw.project` object provides access to project-level settings and metadata.

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `title` | String | The project title |
| `mode` | String | Current mode: `"edit"` or `"preview"` |
| `siteUrl` | String | The site's base URL |
| `language` | String | Project language code (e.g., `"en"`) |
| `enableSocialTags` | Boolean | Whether social tags are enabled |
| `allowDarkMode` | Boolean | Whether dark mode is enabled |
| `logo.url` | String | Path to the project logo |
| `logo.alt` | String | Alt text for the project logo |

## Accessing Project Data

```javascript
const transformHook = (rw) => {
    const { title, mode, siteUrl, language } = rw.project;
    
    console.log(title);    // "My Website"
    console.log(mode);     // "edit" or "preview"
    console.log(siteUrl);  // "https://example.com"
    console.log(language); // "en"
};

exports.transformHook = transformHook;
```

## Edit vs Preview Mode

One of the most common uses is detecting the current mode:

```javascript
const transformHook = (rw) => {
    const { mode } = rw.project;
    
    const isEditMode = mode === 'edit';
    const isPreviewMode = mode === 'preview';
    
    // Show placeholder content in edit mode
    const placeholderImage = isEditMode 
        ? '/path/to/placeholder.png' 
        : null;
    
    rw.setProps({
        isEditMode,
        isPreviewMode,
        placeholderImage
    });
};

exports.transformHook = transformHook;
```

## Accessing the Project Logo

```javascript
const transformHook = (rw) => {
    const { logo, title } = rw.project;
    
    rw.setProps({
        logoUrl: logo.url,
        logoAlt: logo.alt || title,
        hasLogo: !!logo.url
    });
};

exports.transformHook = transformHook;
```

## Passing Project Data to Templates

```javascript
const transformHook = (rw) => {
    rw.setProps({
        project: rw.project
    });
};

exports.transformHook = transformHook;
```

In templates:

```html
<title>{{project.title}}</title>
<html lang="{{project.language}}">

@if(project.logo.url)
    <img src="{{project.logo.url}}" alt="{{project.logo.alt}}">
@endif
```
