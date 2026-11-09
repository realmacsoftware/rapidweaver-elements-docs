# rw.page

The `rw.page` object provides access to information about the current page where the component is placed.

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `id` | String | Unique identifier for the page (e.g., `"page0"`) |
| `title` | String | The page title |
| `description` | String | Page description/meta description |
| `filename` | String | The page filename (e.g., `"index.html"`) |
| `ext` | String | File extension (e.g., `"html"`) |
| `language` | String | Page language code (e.g., `"en"`) |
| `absolutePath` | String | Full path to the page |
| `docRootPath` | String | Path to document root |
| `projectResourcesPath` | String | Path to project resources folder (e.g., `"resources"`) |
| `isFolder` | Boolean | Whether this represents a folder |
| `displayInMenu` | Boolean | Whether to show in navigation |
| `isDraft` | Boolean | Draft pages are not published |
| `icon` | Object | Page icon object |

## Example Object

```javascript
{
    "id": "page0",
    "title": "About",
    "description": "",
    "filename": "index.html",
    "ext": "html",
    "language": "en",
    "absolutePath": "",
    "docRootPath": "",
    "projectResourcesPath": "resources",
    "isFolder": false,
    "displayInMenu": true,
    "isDraft": false,
    "icon": {}
}
```

## Accessing Page Data

```javascript
const transformHook = (rw) => {
    const { 
        id, 
        title, 
        filename, 
        absolutePath,
        language 
    } = rw.page;
    
    console.log(id);           // "page0"
    console.log(title);        // "About"
    console.log(filename);     // "index.html"
    console.log(absolutePath); // ""
    console.log(language);     // "en"
};

exports.transformHook = transformHook;
```

## Checking Page Status

```javascript
const transformHook = (rw) => {
    const { isFolder, isDraft, displayInMenu } = rw.page;
    
    if (isDraft) {
        console.log("This page is a draft");
    }
    
    if (isFolder) {
        console.log("This is a folder page");
    }
    
    rw.setProps({
        showInNav: displayInMenu && !isDraft
    });
};

exports.transformHook = transformHook;
```

## Using Page Paths

```javascript
const transformHook = (rw) => {
    const { absolutePath, projectResourcesPath } = rw.page;
    
    rw.setProps({
        currentPath: absolutePath,
        resourcesPath: projectResourcesPath
    });
};

exports.transformHook = transformHook;
```

## Passing Page Data to Templates

```javascript
const transformHook = (rw) => {
    rw.setProps({
        page: rw.page
    });
};

exports.transformHook = transformHook;
```

In templates:

```html
<h1>{{page.title}}</h1>
<html lang="{{page.language}}">

@if(page.description)
    <meta name="description" content="{{page.description}}">
@endif
```
