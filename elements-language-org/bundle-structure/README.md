---
description: An Element Pack is a bundled folder
icon: box
---

# Element Pack

The Element Pack format is a highly versatile folder based plugin format for sharing and distributing  addons for Elements.

Element Packs are essentially a collection of folders and files, with the top-level directory having a name that ends with a `.elementsdevpack` extension. This name and structure is only used for development purposes, dev element packs should not be sold or distributed to other users.

An Element Pack can contain one or more add-on types, including any combination of the following:

* Components
* Resources
* Templates
* Themes
* Projects (planned)

Templates, Resources, and Themes should be built inside of Elements. However, Components require a specific directory structure in order to work correctly, these are called Bundles in macOS, and need to be built outside of Elements.

Element Packs distributed via the Elements Store and encrypted and non-editable meaning your code is protected. You can [learn more about distributing your addons here](../../elements-marketplace/distribution.md).

### Element Dev Pack Bundle Structure

The following outlines the top level folder structure for an Element Pack. It can contain multiple addons, each component or theme should be placed in the corresponding folders inside the pack.

* MyElementPack.elementsdevpack (folder/bundle)
  * components (folder)
  * [info.json (file)](info.json.md)
  * themes (folder)
  * [shared (folder)](components/shared-files/)

The following shows an Element Dev Pack containing multiple themes and components:

* MyElementPack.elementsdevpack (bundle)
* info.json
* components (folder)
  * com.companyname.slideshow (folder)
  * com.companyname.navbar (folder)
* themes (folder)
  * com.companyname.themes.architect (folder)
  * com.companyname.themes.solar (folder)
* shared (folder)



