# rw.pages

The `rw.pages` array provides access to the site's navigation structure. This is commonly used for building navigation menus, sitemaps, and breadcrumbs.

## Properties

Each page object in the array contains:

| Property | Type | Description |
|----------|------|-------------|
| `title` | String | The page title |
| `url` | String | Relative URL to the page (e.g., `"portfolio/"`) |
| `description` | String | Page description |
| `isPage` | Boolean | Whether this is a regular page |
| `isFolder` | Boolean | Whether this is a folder |
| `isLink` | Boolean | Whether this is an external link |
| `isCode` | Boolean | Whether this is a code file |
| `isExternal` | Boolean | Whether this links externally |
| `isActive` | Boolean | Whether this is the current page |
| `hasActiveChild` | Boolean | Whether a child page is active |
| `isDraft` | Boolean | Draft pages are not published |
| `displayInMenu` | Boolean | Whether to show in navigation |
| `openInNewWindow` | Boolean | Whether link opens in new window |
| `navLevel` | Number | Navigation depth level (0 = top level) |
| `pageDepth` | Number | Depth in page hierarchy |
| `hasPages` | Boolean | Whether this page has child pages |
| `pages` | Array | Nested array of child pages |
| `icon` | Object | Page icon object |

## Example Structure

```javascript
[
    {
        "title": "About",
        "url": "./",
        "description": "",
        "isPage": true,
        "isFolder": false,
        "isLink": false,
        "isCode": false,
        "isExternal": false,
        "isActive": true,
        "hasActiveChild": false,
        "isDraft": false,
        "displayInMenu": true,
        "openInNewWindow": false,
        "navLevel": 0,
        "pageDepth": 0,
        "hasPages": false,
        "pages": [],
        "icon": {}
    },
    {
        "title": "Portfolio",
        "url": "portfolio/",
        "description": "",
        "isPage": true,
        "isFolder": false,
        "isLink": false,
        "isCode": false,
        "isExternal": false,
        "isActive": false,
        "hasActiveChild": false,
        "isDraft": false,
        "displayInMenu": true,
        "openInNewWindow": false,
        "navLevel": 0,
        "pageDepth": 1,
        "hasPages": true,
        "pages": [
            {
                "title": "Project Template",
                "url": "portfolio/project1/",
                "navLevel": 1,
                "pageDepth": 2,
                "hasPages": false,
                "pages": [],
                // ... other properties
            }
        ],
        "icon": {}
    }
]
```

## Accessing Pages

```javascript
const transformHook = (rw) => {
    const pages = rw.pages;
    
    console.log(pages.length);        // Number of top-level pages
    console.log(pages[0].title);      // "About"
    console.log(pages[0].isActive);   // true (if current page)
};

exports.transformHook = transformHook;
```

## Filtering for Navigation

Filter pages to only show those meant for navigation:

```javascript
const transformHook = (rw) => {
    const filterPages = (pages) => {
        return pages
            .filter(page => page.displayInMenu && !page.isDraft)
            .map(page => ({
                ...page,
                pages: page.hasPages ? filterPages(page.pages) : []
            }));
    };
    
    const navPages = filterPages(rw.pages);
    
    rw.setProps({
        navPages,
        hasNavPages: navPages.length > 0
    });
};

exports.transformHook = transformHook;
```

## Building a Navigation Menu

```javascript
const transformHook = (rw) => {
    const filterPages = (pages) => {
        return pages
            .filter(page => page.displayInMenu && !page.isDraft)
            .map(page => ({
                ...page,
                hasPages: page.pages ? filterPages(page.pages).length > 0 : false,
                pages: page.pages ? filterPages(page.pages) : []
            }));
    };
    
    const pages = filterPages(rw.pages);
    
    rw.setProps({
        pages,
        hasPages: pages.length > 0
    });
};

exports.transformHook = transformHook;
```

Template for navigation:

```html
<nav>
    <ul>
        @each(page in pages)
            <li class="@if(page.isActive)active@endif">
                <a href="{{page.url}}" 
                   @if(page.openInNewWindow)target="_blank"@endif>
                    {{page.title}}
                </a>
                
                @if(page.hasPages)
                    <ul>
                        @each(subPage in page.pages)
                            <li class="@if(subPage.isActive)active@endif">
                                <a href="{{subPage.url}}">{{subPage.title}}</a>
                            </li>
                        @endeach
                    </ul>
                @endif
            </li>
        @endeach
    </ul>
</nav>
```

## Finding the Active Page

```javascript
const transformHook = (rw) => {
    const findActivePage = (pages) => {
        for (const page of pages) {
            if (page.isActive) return page;
            if (page.hasActiveChild && page.pages) {
                const active = findActivePage(page.pages);
                if (active) return active;
            }
        }
        return null;
    };
    
    const activePage = findActivePage(rw.pages);
    
    rw.setProps({
        activePage,
        activePageTitle: activePage?.title || ''
    });
};

exports.transformHook = transformHook;
```

## Building Breadcrumbs

```javascript
const transformHook = (rw) => {
    const buildBreadcrumbs = (pages, trail = []) => {
        for (const page of pages) {
            if (page.isActive) {
                return [...trail, page];
            }
            if (page.hasActiveChild && page.pages) {
                const result = buildBreadcrumbs(page.pages, [...trail, page]);
                if (result) return result;
            }
        }
        return null;
    };
    
    const breadcrumbs = buildBreadcrumbs(rw.pages) || [];
    
    rw.setProps({
        breadcrumbs,
        hasBreadcrumbs: breadcrumbs.length > 1
    });
};

exports.transformHook = transformHook;
```

## Checking for Subpages

```javascript
const transformHook = (rw) => {
    const pages = rw.pages;
    
    // Find pages with children
    const pagesWithChildren = pages.filter(page => page.hasPages);
    
    // Get all top-level page titles
    const pageTitles = pages.map(page => page.title);
    
    rw.setProps({
        pagesWithChildren,
        pageTitles,
        totalPages: pages.length
    });
};

exports.transformHook = transformHook;
```
