---
icon: circle-question
---

# What is a Component?

A component is a self-contained, reusable building block that can be added to a page in the Elements app. It encapsulates its own layout (templates), configuration options (properties), and logic (hooks). Each component lives in its own folder within an Element Pack and follows a strictly defined structure.

### Folder Structure Overview

Each component is self-contained: all templates, assets, and logic should live within a single folder. You should use a reverse domain name (e.g., `com.companyname.componentname`) as the component directory name.

```
components/
├── com.companyname.slideshow/
│   ├── info.json
│   ├── properties.json
│   ├── properties.config.json
│   ├── hooks.js
│   ├── hooks.source.js
│   ├── icon.pdf
│   ├── icon-dark.pdf
│   ├── paletteIcon.pdf
│   ├── paletteIcon-dark.pdf
│   ├── collections/
│   │   └── *.json
│   ├── templates/
│   │   ├── index.html
│   │   ├── backend/
│   │   ├── pageStart/
│   │   ├── pageEnd/
│   │   ├── bodyStart/
│   │   ├── bodyEnd/
│   │   ├── includes/
│   │   ├── *.html
│   │   ├── *.php
│   │   ├── *.css
│   │   └── *.js
│   └── assets/
├── com.companyname.navbar/
│   └── ...
└── shared/
    ├── assets/
    └── templates/
```

### Component File Breakdown

Below is a detailed breakdown of the files that make up a component and how they function together.

#### [info.json](info.json.md) (required)

The "manifest" file that defines the component's metadata, such as its unique identifier, title, author, group, and icons. It tells Elements how to identify and display the component in the UI.

#### [properties.json](properties.json/) (required)

Defines the configurable options (controls) that users see in the inspector when using the component. This file maps user settings to values that can be used in templates and hooks.

#### [properties.config.json](../development-resources/build-tools/#controls-in-propertiesconfigjson) (optional)

Used in conjunction with [Build Tools](../development-resources/build-tools/) to simplify property definitions. It allows you to use `globalControl` references to include standardized UI controls (like spacing, sizing, or background) without redefining them in every component.

#### [hooks.js](hooks.js/)

A JavaScript file where you can define logic, data handling, or custom behavior for the component. It runs during the build process and can manipulate data before it's passed to the templates.

#### [hooks.source.js](../development-resources/build-tools/#shared-hooks-in-hookssourcejs) (optional)

The source JavaScript file used by [Build Tools](../development-resources/build-tools/) to generate the final `hooks.js`. This is often used when you want to use modern JavaScript features or shared utility functions.

#### [icon.pdf, icon-dark.pdf, paletteIcon.pdf, paletteIcon-dark.pdf](icons.md)

The visual representation of the component. `icon.pdf` is the main icon, while `paletteIcon.pdf` is used specifically in the component palette. Dark mode versions are provided for better visibility in different UI themes.

#### [collections/](collections/)

Contains JSON files that define structured data groups or sub-items for the component. For example, an accordion component might have a collection of items, each with its own title and content.

#### [templates/](language/)

Contains the files that define how the component is rendered. All files in this folder are processed using the [Elements Template Language](language/).

* **index.html**: Usually the main entry point for the component's HTML output.
* **\*.html / \*.php**: The component's markup. Files are processed, concatenated, and added to the page.
* **\*.css**: All CSS files are processed, concatenated, and added to the page's stylesheet during publishing.
* **\*.js**: All JavaScript files are processed, concatenated, and added to the page's script file during publishing.
* [**includes/**](language/include.md): Sub-templates that can be reused across multiple templates using the `@include` directive.
* [**headStart/, headEnd/, bodyStart/, bodyEnd/, pageStart/, pageEnd/**](templates/): Templates in these folders are automatically injected into specific regions of the final HTML document.
* [**backend/**](templates/backend.md): Files that should be deployed to the server but are not directly included in the page (e.g., PHP processing scripts).

#### [assets/](assets.md)

Contains supporting files like images, raw CSS, or static JavaScript that should **not** be processed by the Elements template language. These files are copied as-is to the exported project.
