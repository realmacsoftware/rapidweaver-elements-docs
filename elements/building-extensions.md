---
description: An overview of the Elements API and the ways you can build components and add-ons
icon: puzzle-piece-simple
---

# Elements API

The Elements API is the developer system used to create components for RapidWeaver Elements. It combines the **Elements Language**, a lightweight HTML templating language, with Inspector properties, build-time JavaScript hooks, styles, client-side scripts, assets, and reusable component files.

You can start with a project-specific Custom Component inside Elements, then move to an Element Dev Pack when you need a reusable package with multiple components, files, icons, collections, or shared assets.

[Open the complete Elements API reference](https://docs.realmacsoftware.com/elements-docs/elements-language)

{% hint style="info" %}
The Elements API is the same component system used by the components supplied with Elements. The [open-source Core Components](https://docs.realmacsoftware.com/elements-docs/elements-language/dev-resources/open-source-components) provide complete production examples.
{% endhint %}

### What You Can Build

The API can be used to create:

* Project-specific Custom Components.
* Reusable components with editable text and child-component dropzones.
* Theme-aware Inspector controls for colours, fonts, spacing, sizing, resources, switches, selections, and other values.
* Interactive components using client-side JavaScript or Alpine.js.
* Components with build-time data processing and conditional output.
* Packs containing several components, custom icons, assets, collections, and shared files.
* Add-ons that can be compiled and distributed through the Elements Store.

### Choose a Development Path

| Approach | Best for | Where it lives |
| --- | --- | --- |
| [Custom Component](components/custom-components.md) | Learning the API, project-specific HTML, and prototypes | Inside an Elements project |
| Element Dev Pack | Reusable components, multiple files, custom icons, collections, and local development | An editable `.elementsdevpack` folder on your Mac |
| Compiled Element Pack | Sharing or selling a finished pack | A compiled package produced through the Elements Platform |

Custom Components provide Template, Styles, JavaScript, Hooks, and Properties editors directly inside Elements. They are the quickest way to learn how properties, dropzones, templates, and hooks work together.

Dev Packs use the same ideas in a file-based project that can contain one or more components. They support live development in Elements and can include files that are not available inside a Custom Component.

{% hint style="warning" %}
Element Dev Packs are editable development bundles and should not be sold or distributed directly. Compile a finished Dev Pack into an Element Pack through the Elements Platform before sharing or selling it.
{% endhint %}

### How a Component Works

A typical component moves through four stages:

1. **Properties** define the controls shown in the Inspector and provide the values selected by the site author.
2. **Hooks** can validate, combine, or transform those values at build time.
3. **Templates** use HTML, property values, and Elements Language directives to generate the component’s output.
4. **Styles, assets, and client-side JavaScript** control the published appearance and browser behaviour.

Simple components may only need a Template. More advanced components can add properties and hooks without changing the authoring experience for the person building the website.

### The Elements Language

The Elements Language keeps component templates close to normal HTML. Property values are inserted with double curly braces:

```html
<h2 class="{{headingColor}}">{{title}}</h2>
```

Directives add editable content and component behaviour:

* `@text`, `@richtext`, and `@markdown` create editable content areas.
* `@dropzone` allows other Elements components to be placed inside a component.
* `@if`, `@elseif`, and `@else` conditionally generate markup.
* `@each` loops over collections and other repeated values.
* `@include` and `@template` organise reusable markup.
* `@portal` places scripts, styles, or markup in another page location.
* `@anchor` creates linkable anchor points.

See the [Elements Language reference](https://docs.realmacsoftware.com/elements-docs/elements-language/component/language) for the complete syntax.

### Inspector Properties

Properties turn a coded component into something that can be configured visually in Elements. Each property has an identifier and a control type, and can provide a formatted value for the Template or Hooks.

For example, a theme colour property can generate a utility class:

```json
{
    "title": "Text Color",
    "id": "textColor",
    "format": "text-{{value}}",
    "themeColor": {
        "default": {
            "name": "text",
            "brightness": 700
        }
    }
}
```

The Template can then use `{{textColor}}` wherever the generated class is needed.

The [Properties reference](https://docs.realmacsoftware.com/elements-docs/elements-language/component/properties-json) documents the available Inspector controls, values, defaults, visibility rules, and responsive behaviour.

### Build-Time Hooks

Hooks are JavaScript functions that run while Elements prepares a component. They are useful for processing values, preparing classes, calculating derived data, and keeping complex logic out of the HTML Template.

```javascript
const transformHook = (rw) => {
    const { firstName, lastName } = rw.props;

    rw.setProps({
        fullName: `${firstName} ${lastName}`
    });
};

exports.transformHook = transformHook;
```

The Template can then output `{{fullName}}`. See the [Hooks reference](https://docs.realmacsoftware.com/elements-docs/elements-language/component/hooks.js) for the build-time API.

### Anatomy of an Element Dev Pack

A Dev Pack can contain:

* Pack metadata and a unique identifier.
* One or more component folders.
* Component metadata in `info.json`.
* Inspector property definitions.
* One or more HTML templates.
* Build-time hooks.
* Component icons and palette icons.
* Page assets such as JavaScript, CSS, images, or fonts.
* Collections for repeatable, structured items.
* Shared files used by several components in the same pack.

The exact structure depends on the component. Start with the generated boilerplate, then add only the files the pack needs.

### Requirements

You need:

* A copy of RapidWeaver Elements.
* A basic understanding of HTML.

CSS, JavaScript, and JSON become useful as components grow more advanced. A code editor is recommended for Dev Packs; the official guide uses standard editors such as Visual Studio Code, Nova, or BBEdit.

The optional [RW Elements Tools](https://docs.realmacsoftware.com/elements-docs/elements-language/dev-resources/build-tools) package provides build helpers, reusable controls, shared properties, and hook utilities for larger component projects.

### Getting Started

1. Build a small [Custom Component](components/custom-components.md) if you want to learn inside an existing project.
2. Follow the [API Quickstart](https://docs.realmacsoftware.com/elements-docs/elements-language/getting-started/getting-started) to create and install an Element Dev Pack.
3. Explore the [official example Dev Packs](https://github.com/realmacsoftware/RWElementDevPacks/tree/main) and [open-source Core Components](https://docs.realmacsoftware.com/elements-docs/elements-language/dev-resources/open-source-components).
4. Add properties, editable content, and dropzones before introducing complex JavaScript.
5. Test several component instances, every breakpoint, keyboard interaction, and the published output.
6. Read the [Store distribution guide](https://docs.realmacsoftware.com/elements-docs/store/partners/pack-distribution) before sharing or selling a finished pack.

### API Reference

* [Elements API overview](https://docs.realmacsoftware.com/elements-docs/elements-language)
* [Quickstart](https://docs.realmacsoftware.com/elements-docs/elements-language/getting-started/getting-started)
* [Elements Language](https://docs.realmacsoftware.com/elements-docs/elements-language/component/language)
* [Properties](https://docs.realmacsoftware.com/elements-docs/elements-language/component/properties-json)
* [Templates](https://docs.realmacsoftware.com/elements-docs/elements-language/component/templates)
* [Hooks](https://docs.realmacsoftware.com/elements-docs/elements-language/component/hooks.js)
* [Assets](https://docs.realmacsoftware.com/elements-docs/elements-language/component/assets)
* [Collections](https://docs.realmacsoftware.com/elements-docs/elements-language/component/collections)
* [Shared Files](https://docs.realmacsoftware.com/elements-docs/elements-language/component/shared-files)
* [Build Tools](https://docs.realmacsoftware.com/elements-docs/elements-language/dev-resources/build-tools)
* [Component Development Forum](https://forums.realmacsoftware.com/c/rapidweaver-elements/custom-components/56)

### Distribution

Use a Dev Pack for development and testing. When a pack is ready to share or sell, compile it through the Elements Platform and follow the Store requirements for packaging, product information, testing, and submission.

The [Store distribution guide](https://docs.realmacsoftware.com/elements-docs/store/partners/pack-distribution) explains the release path for finished Element Packs.
