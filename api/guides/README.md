---
description: >-
  Learn how real Elements components combine properties, hooks, collections,
  and templates — through guided tours of the open-source Core Pack.
icon: graduation-cap
---

# Building Complex Components

The reference documentation tells you what each part of the Elements API does — every `rw` method, every directive, every property control. These guides answer the other question: how do real components combine those pieces into something you'd actually ship? Each guide dissects one or more components from the open-source [Core Pack](../development-resources/open-source-components.md), so you can read the explanation with the shipping source open beside it.

### What Makes a Component Complex?

A simple component is one template and a handful of properties. A complex component coordinates several files, each with a distinct job. Here is the real file tree of the core **Tabs** component (`com.realmacsoftware.tabs`):

```
com.realmacsoftware.tabs/
├── info.json                  # Manifest: identifier, title, group, and icon name
├── properties.config.json     # Source property definitions, using shared globalControl references
├── properties.json            # Generated inspector controls, built from properties.config.json
├── hooks.source.js            # Source build-time logic — the file you actually edit
├── hooks.js                   # Generated hooks bundle that Elements runs at build time
├── icon.pdf                   # Component icon shown in the editor
├── paletteIcon.pdf            # Smaller icon shown in the component palette
├── collections/
│   └── tabs/                  # Defines the repeatable "tab" items users add in the inspector
│       ├── info.json          # The collection's identifier and title
│       ├── defaults.json      # The three starter tabs every new Tabs component begins with
│       └── properties.json    # Inspector controls for each individual tab item
└── templates/
    ├── index.html             # Main markup: loops the tabs and renders a dropzone per panel
    ├── alpine.html            # Portal that registers the shared Alpine.js tabs behaviour once
    └── editor-ui.css          # Edit-mode-only CSS that reveals whichever panel is being edited
```

Two of these files you never touch directly: `properties.json` is generated from `properties.config.json`, and `hooks.js` is generated from `hooks.source.js` by the Core Pack's [Build Tools](../development-resources/build-tools/README.md). The source files stay small and readable; the generated files are what Elements loads. Complexity, in other words, isn't more code in one file — it's more files doing one job each.

{% hint style="info" %}
The Core Pack is a working reference for every pattern in these guides. Each guide names the components it dissects, so you can open the real source in your editor and follow along file by file.
{% endhint %}

### The Three Runtimes You Write For

A component this size runs code in up to three different places, and keeping them straight is the single most useful mental model in these guides.

**Build-time JavaScript (`hooks.js`).** This code runs inside Elements while the page is generated — never in the browser. There is no `require` or `import`; everything happens through the [`rw` object](../component/hooks.js/README.md): read the user's settings from `rw.props`, compute derived values, and pass results to your templates with `rw.setProps`. If a value can be decided before the page is published, decide it here.

**Browser JavaScript.** Anything interactive — switching tabs, opening modals, animating on scroll — ships to the visitor's browser through your [templates](../component/language/README.md), usually via a portal. The Core Pack standardises on Alpine.js: each component registers its behaviour once in a `bodyEnd` portal, then binds it declaratively in the markup.

**Server-side PHP (optional).** A few components do work at request time, after publishing. The core Table component's main template is `index.php`, letting the published page process data on the server each time it's requested. Most components never need this runtime, but when you do, Elements treats `.php` templates as first-class citizens.

### Guide Map

Start with the tutorial if you're building your first non-trivial component, or jump straight to the guide that matches the problem in front of you.

| Guide                                                                                                | What you'll learn                                                                    | Dissects                          |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | --------------------------------- |
| [Tutorial: Build an FAQ Component](tutorial/README.md)                                                | A four-part, end-to-end walkthrough from empty folder to finished component          | Built from scratch                |
| [Interactive Components with Alpine.js](interactive-components-with-alpine.md)                        | Registering shared Alpine behaviour via portals and binding state in your markup     | Accordion, Tabs, Content Slider   |
| [Modals, Overlays & Portals](modals-overlays-and-portals.md)                                          | Rendering overlay markup outside your component and wiring open/close triggers       | Modal, Modal Close                |
| [Collection-Driven Dropzones](collection-driven-dropzones.md)                                         | Pairing user-editable collections with `@each` loops and per-item dropzones          | Tabs, Table                       |
| [Component Suites & Cross-Component Communication](component-suites.md)                               | Building families of components that discover and talk to each other                 | Filter, Filter Tags, Modal, Reveal |
| [Designing the Edit-Mode Experience](edit-mode-experience.md)                                         | Using `@if(edit)`, editor-only CSS, and editor properties to make editing pleasant   | Table, Tabs, Gallery              |
| [Integrating JavaScript Libraries](integrating-javascript-libraries.md)                               | Bundling a third-party library and initialising it safely with portals               | Reveal, Gallery                   |
| [Responsive Images & Media](responsive-images-and-media.md)                                           | Resource properties, responsive values, and media that adapts across breakpoints     | Image, Text Wrap, Container       |
| [Galleries & Resource Collections](galleries-and-resource-collections.md)                             | Managing many images at once with collections of resources                           | Gallery                           |
| [Server-Side PHP Components](server-side-php-components.md)                                           | Emitting PHP templates that run on the server at request time                        | Table                             |
| [Building Form Components](building-form-components.md)                                              | A worked architecture for inputs, validation, and submission handling                | Generic worked example            |
| [External Data Sources](external-data-sources.md)                                                     | Pulling remote data into a component and rendering it                                | Table                             |
| [Navigation & Recursive Templates](navigation-and-recursive-templates.md)                             | Walking the page tree and rendering nested menus with recursive includes             | Nav Tree, Menu                    |

{% content-ref url="tutorial/README.md" %}
[Start here if you're new — build a complete FAQ component step by step.](tutorial/README.md)
{% endcontent-ref %}

## Related Documentation

* [What is a Component?](../component/components.md)
* [Hooks Reference](../component/hooks.js/README.md)
* [Elements Template Language](../component/language/README.md)
* [Open Source Core Components](../development-resources/open-source-components.md)
* [Getting Started](../getting-started/getting-started.md)
