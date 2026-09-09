---
description: Translate RapidWeaver Classic and Stacks terminology into Elements
---

# The Phrasebook

Elements is a completely new website builder, so some familiar RapidWeaver Classic and Stacks terms have changed. Much of what you already know still applies, but the tools may have a different name or be organised in a different way.

Use this phrasebook to translate an old workflow into its Elements equivalent.

{% hint style="info" %}
Not every Classic feature has a one-to-one replacement. Where the workflow has changed, this page points you towards the closest Elements approach.
{% endhint %}

## The five translations to learn first

### Stacks → Components

In Classic, you dragged stacks onto a Stacks page to build a layout. In Elements, you drag [Components](../elements/components/) directly onto any page, then arrange and nest them on the live canvas.

The basic idea is familiar, but Components are part of the core Elements workflow. Built-in, Store, third-party, and custom Components all use the same canvas, Inspector, responsive controls, Theme values, and Resources system.

### Partials → Globals

A Stacks Partial becomes a [Global](../elements/global-templates.md). Globals are linked groups of Components that you can place on several pages. Update the Global once and every linked instance updates.

Use Globals for menus, headers, footers, announcements, and other content that should remain consistent throughout a site. Individual instances can expose overrides when one page needs different text or imagery.

### Themes and Master Styles → Theme Studio

Classic themes supplied the overall design and offered a fixed set of variations through Master Styles. Elements gives you direct control through [Theme Studio](../elements/theme-studio/README.md).

Theme Studio holds the reusable colours, fonts, text sizes, spacing, borders, radii, shadows, and responsive screens for your project. Components use these shared values, so changing a Theme value can update the design throughout your site.

There is no direct equivalent to installing a Classic theme. Start with Elements Components and [Templates](../elements/templates.md), then shape the design with Theme Studio.

### Page types → Pages built from Components

Classic often used a different plug-in page type for each kind of content. In Elements, most pages use the same visual canvas and are assembled from Components.

For example, build a photo page with a Gallery component, a contact page with Form components, or an article with Text, Typography, Image, and Markdown components. Elements can also create code and Markdown files when you need to work directly with source content.

### Edit and Preview → Live canvas and Browser Preview

Classic separated editing from Preview. Elements shows the page visually while you build it, so most design changes appear immediately on the canvas.

Use [Browser Preview](../elements/previewing-your-website.md) when you want to test the generated site in a real browser, check links and interaction, or compare responsive layouts outside the editor.

## Page building and reusable content

| In Classic or Stacks | In Elements | What it means |
| --- | --- | --- |
| Stack | [Component](../elements/components/) | A building block such as Text, Image, Button, Grid, or Form. |
| Stacks library | Components panel | The place you browse and drag Components from. |
| Stacks page | Page | Every standard Elements page can be built visually from Components. |
| Partial | [Global](../elements/global-templates.md) | Linked content that updates everywhere it is used. |
| Saved layout or reusable section | [Template](../elements/templates.md) | A reusable starting point that becomes an independent copy when added. |
| Columns stack | [Grid](../elements/components/grid.md) or [Flex](../elements/components/flex.md) | Layout Components for arranging content in rows and columns. |
| Site-wide stack or shared layout | Global | Use when every placed instance should remain linked. |
| Third-party stack | Store or custom Component | Install an Elements version from the Store, or build a custom Component. |
| Foundry, Foundation, or another framework | Components and Theme Studio | Elements has its own integrated layout and design system. |

{% hint style="info" %}
[Templates and Globals](../elements/reusable-content.md) solve different problems. A Template creates an independent copy; a Global remains linked to its source.
{% endhint %}

## Design and responsive layout

| In Classic or Stacks | In Elements | What it means |
| --- | --- | --- |
| Theme | Theme Studio and Templates | Theme Studio controls shared design values; Templates provide ready-made layouts. |
| Master Styles or Site Styles | [Theme Studio](../elements/theme-studio/README.md) | Change the design system used throughout the project. |
| Theme or stack style variation | Theme value or Component setting | Choose a shared Theme value or customise the selected Component in the Inspector. |
| Breakpoint | [Breakpoint](../elements/responsive-breakpoints.md) | Adjust layouts for different screen widths using mobile-first overrides. |
| Device Simulator | Breakpoint controls and Browser Preview | Design at chosen widths on the canvas, then test in a browser. |
| Hide a stack | Component display mode | Use Hide in Editor, Do Not Publish, or Hide and Do Not Publish as required. |
| Edit mode | Editor canvas | Build and style the page visually. |
| Preview mode | Live canvas or Browser Preview | The canvas updates while you work; Browser Preview tests the generated site. |

## Content, images, and resources

| In Classic or Stacks | In Elements | What it means |
| --- | --- | --- |
| Styled Text page | Text and Typography Components | Add editable text to a visual page. |
| HTML page | Code file or Components | Work directly with source when needed, or recreate the page visually. |
| Markdown page | Markdown Component or Markdown file | Display Markdown on a page or maintain Markdown as a project file. |
| Photo Album page | [Gallery](../elements/components/gallery.md) | Build a media gallery from a Resources folder. |
| Contact Form page or form stack | [Form Components](../elements/components/form/README.md) | Assemble the fields and behaviour required by the form. |
| Site Image or image stack | [Image Component](../elements/components/image.md) | Display a project Resource, custom URL, or CMS image. |
| Resources Browser | [Resources](../elements/resources.md) | Manage images, fonts, documents, media, and folders used by the project. |
| Warehouse image or warehousing images | Remote Resource or Custom image URL | Reference an image that remains hosted at an external URL. |
| Media Inspector | Resource Info or Image Inspector | Edit resource metadata, or configure a Custom or CMS image on its Component. |

## Projects, pages, and publishing

| In Classic | In Elements | What it means |
| --- | --- | --- |
| Page List | [Page Manager](../elements/page-manager.md) | Create, organise, rename, and move pages and folders. |
| Page Inspector | Page settings and Inspector | Configure the page or edit the currently selected Component. |
| Site Setup | [Project Settings](../elements/site-settings/README.md) | Manage project-wide details such as the site address, icons, and advanced settings. |
| Plug-in page | Page built from Components or a code file | Choose the Components needed for the page rather than installing a page type. |
| Publishing Method | Publishing destination | Store the connection details for a server or local publishing location. |
| Export | Publish to a local folder | Generate the website in a folder on your Mac. |
| RapidWeaver project | Elements project | The editable project containing your pages, design system, settings, and Resources. |

## Familiar terms that remain

Some names require little or no translation:

* **Inspector** is still the Inspector. It changes according to the page or Component you select.
* **Pages** and **folders** still define the structure of your website.
* **Resources** still hold the files used by the project, although Elements adds richer folders, metadata, and remote-resource workflows.
* **Browser Title**, **Meta Description**, and other SEO fields serve the same purpose.
* **Publishing** still generates your site and sends it to the destination you configure.

## Translating common Classic workflows

### Reusing a header or footer

Build the layout from Components, convert it to a Global, and place that Global on each page. Later changes to the Global appear in every linked instance.

### Starting from a pre-built design

Choose an Elements Template for the page or section you need. Once added, it becomes an independent group of Components that you can customise. Use Theme Studio to adapt the colours, typography, spacing, and other shared design values.

### Using a warehouse image

For an image you will reuse, add its URL through **Add Remote Resources**. For a one-off image, choose **Custom** in the Image Component and enter its URL directly. See [Resources](../elements/resources.md#adding-remote-resources-warehouse-images) for both workflows and alternative-text guidance.

### Replacing a specialist page plug-in

Start with a regular page and add the Components that provide the required content and behaviour. Check the built-in Components and Elements Store first. If the feature is unique, you can create a custom Component rather than relying on a special page type.

## What does not carry over

Classic themes, plug-ins, and Stacks add-ons cannot be installed in Elements. They were built for a different editor and rendering system. Rebuild their layouts with Elements Components, look for an equivalent in the Elements Store, or create a custom Component.

The [Classic Project Importer](import-classic-projects.md) can transfer page structure, settings, Resources, and some content, but it does not reproduce an existing theme or every third-party stack. Treat an imported project as a starting point for rebuilding the design in Elements.

## Where to go next

* Follow the [Quickstart](../getting-started/quickstart.md) to build a small Elements site.
* Read [Core Concepts](../getting-started/design-system.md) for Projects, Themes, Components, Templates, and Globals.
* Learn when to use [Templates and Globals](../elements/reusable-content.md).
* Review the [Classic Project Importer](import-classic-projects.md) before moving an existing site.
