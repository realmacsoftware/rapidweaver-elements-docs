---
description: Import your RapidWeaver Classic Project into Elements
icon: arrow-down-to-bracket
---

# Importing Projects



{% hint style="danger" %}
Please note this documentation is a work-in-progress…
{% endhint %}

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

In Elements [we use Globals](../editor/global-templates.md) instead, these are a highly modern and customisable way to include global content throughtout your website.
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
* 1col > Grid
* Header > Text
* Header Pro > Text
* Text > Text
* Picture > Image\
