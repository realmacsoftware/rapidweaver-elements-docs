---
description: Import your RapidWeaver Classic Project into Elements
icon: arrow-down-to-bracket
---

# Import Classic Projects

The Classic Project Importer is an experimental feature. It can bring over the page structure and settings from your Classic project, but content import is less reliable because many page types cannot be mapped directly to Elements components.

{% hint style="danger" %}
**This is an experimental feature!** Please read the full document before importing a project.
{% endhint %}

Keep in mind this tool is designed to **help you move content across, not to recreate your site’s design**. You will need to rebuild the layout and styling using Elements components. Think of it as a way to save time copying text, images, and page structures rather than a one-click migration.

If you’re planning a move from Classic, we strongly recommend reading the rest of the documentation to understand how Elements works, what can be imported, and what you’ll need to redesign.

Watch the video's below to learn more about importing Classic Projects to Elements.

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Dev Daiary 96</strong></td><td>How to  Import Classic Projects into Elements.</td><td><a href="../../../.gitbook/assets/maxresdefault-1.jpg">maxresdefault-1.jpg</a></td><td><a href="https://youtu.be/-Eu-o9zRSmE">https://youtu.be/-Eu-o9zRSmE</a></td></tr><tr><td><strong>Dev Diary 97</strong></td><td>Import Stacks, Foundry, and Foundation based Projects.</td><td><a href="../../../.gitbook/assets/maxresdefault.jpg">maxresdefault.jpg</a></td><td><a href="https://youtu.be/JFymG65pDTw">https://youtu.be/JFymG65pDTw</a></td></tr><tr><td><strong>Stacks to Elements</strong></td><td>Learn the key differences when migrating Projects.</td><td><a href="../../../.gitbook/assets/maxresdefault-2.jpg">maxresdefault-2.jpg</a></td><td><a href="https://youtu.be/28KsND9e6EQ">https://youtu.be/28KsND9e6EQ</a></td></tr></tbody></table>

## Importing a Classic Project

To import a RapidWeaver Classic Project, launch Elements and choose `File > [Beta] Import Classic Project…` from the menu.

## Project Structure

Elements will import all important site information including:

* All Pages (file name, browser title, page name, folder names, etc)
* Page level scripts
* Meta information
* SEO Information
* Robot tags
* Site Settings (Name, site URL, and logo)
* Fav Icons
* Resources (Including Stack page resources)&#x20;
* Publishing Destinations

## Styled Text Page

The text content from Styled Text Pages will be placed into a Typography Component, and any images placed into Image Components.

## HTML and Markdown Pages

These pages will be converted into code pages.

## Photo Album Page

Elements will import photos from each Photo Album page and place them into a folder in the resources area, along with creating a page with a Photo gallery component.

## Stack Plugin Pages

Elements will import Stack pages, and will do it's best to preserve the content from popular stacks and frameworks. However, please remember the importer is for importing content, it will not style any of the imported content or page.

{% hint style="warning" %}
**The Classic Project Importer does not yet read Partials.** To work around this, you may want to unpack any partials and save a copy of your Classic project before you import it into Elements.&#x20;

In Elements [we use Globals](../../../elements/global-templates.md) instead, these are a highly modern and customisable way to include global content throughtout your website.
{% endhint %}

### Stack Resources

Elements will import all Stack Page Resources, it will then optimise the resources by de-duping files to ensure your Elements project and new site is smaller and faster!

### Supported stack Content

Elements currently imports the raw text and image content from a pre-determined list stacks, they are imported with minimal properties (i.e. no colours, or links, etc…).

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
