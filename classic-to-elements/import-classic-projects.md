---
description: Import your RapidWeaver Classic project into Elements
icon: arrow-down-to-bracket
---

# Import Classic Projects

The Classic Project Importer is an experimental feature. It can bring over the page structure and settings from your Classic project, but content import is less reliable because many page types cannot be mapped directly to Elements components.

{% hint style="danger" %}
**This is an experimental feature!** Please read the full document before importing a project.
{% endhint %}

Keep in mind this tool is designed to **help you move content across, not to recreate your site’s design**. You will need to rebuild the layout and styling using Elements components. Think of it as a way to save time copying text, images, and page structures rather than a one-click migration.

If you’re planning a move from Classic, we strongly recommend reading the rest of the documentation to understand how Elements works, what can be imported, and what you’ll need to redesign.

Watch the videos below to learn more about importing Classic projects into Elements.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Dev Diary 96</strong></td><td>How to Import Classic Projects into Elements.</td><td><a href="../.gitbook/assets/maxresdefault-1.jpg">maxresdefault-1.jpg</a></td><td><a href="https://youtu.be/-Eu-o9zRSmE">https://youtu.be/-Eu-o9zRSmE</a></td></tr><tr><td><strong>Dev Diary 97</strong></td><td>Import Stacks, Foundry and Foundation-based Projects.</td><td><a href="../.gitbook/assets/maxresdefault.jpg">maxresdefault.jpg</a></td><td><a href="https://youtu.be/JFymG65pDTw">https://youtu.be/JFymG65pDTw</a></td></tr></tbody></table>

## Importing a Classic Project

To import a RapidWeaver Classic project, launch Elements and choose **File › [Beta] Import Classic Project…**.

## Project Structure

Elements will import all important site information including:

* All pages, including file names, browser titles, page names and folder names
* Page-level scripts
* Meta information
* SEO information
* Robot tags
* Site settings, including the name, site URL and logo
* Favicons
* Resources, including Stack page resources
* Publishing destinations

## Styled Text Page

Text from Styled Text pages is placed in Typography components, while images are placed in Image components.

## HTML and Markdown Pages

These pages will be converted into code pages.

## Photo Album Page

Elements imports photos from each Photo Album page, places them in a folder within Resources and creates a page containing a Photo Gallery component.

## Stack Plugin Pages

Elements imports Stack pages and does its best to preserve content from popular stacks and frameworks. The importer transfers content but does not reproduce the styling of the original page.

{% hint style="warning" %}
**The Classic Project Importer does not yet read Partials.** To work around this, you may want to unpack any partials and save a copy of your Classic project before you import it into Elements.

In Elements, [Globals](../elements/global-templates.md) provide a modern, customisable way to include shared content throughout your website.
{% endhint %}

### Stack Resources

Elements imports all Stack page resources, then removes duplicate files to make the project and published site smaller.

### Supported Stack Content

Elements currently imports raw text and image content from a predefined list of stacks. Content is imported with minimal properties and does not retain colours, links or other styling.

Elements will attempt to import content from the following stacks. Unknown stacks will be converted into named Containers.

#### Built-in Stacks

* Text > Text
* Markdown > Text
* HTML > Text
* Header > Text
* Quote > Text
* Image & Site Image > Image
* Button > Button
* Column stacks will be converted into the Grid Component and use the corresponding number of columns.

#### Foundry 2

* Button > Button
* Container > Container
* Vertical Center > Container
* Header > Text
* Header Plus > Text
* Paragraph > Typography
* Grid Content > Grid
* Image > Image
* Banner > Container
* Margins > Container

#### Foundry 3

* Container > Container
* Columns Grid
* Col > Container
* Header > Text
* Paragraph > Typography
* Image > Image

#### Foundation 6

* Container > Container
* Column stacks > Grid
* Grid stacks > Grid
* Header > Text
* Header Pro > Text
* Text > Text
* Quote > Text
* Label > Text
* Code > Text
* Picture > Image<br>
