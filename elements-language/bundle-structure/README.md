---
description: An Element Pack is a bundled folder
---

# Element Pack

Components and Themes require a specific directory structure in order to work correctly, these are called Bundles in macOS.

Element Packs are bundles are directory hierarchies, with the top-level directory having a name that ends with a `.elementsdevpack` extension.

### Element Dev Pack Bundle Structure

The following outlines the top level folder structure for an Element Pack. It can contain multiple addons, each component or theme should be placed in the corresponding folders inside the pack.

* MyElementPack.elementsdevpack (folder/bundle)
  * components (folder)
  * [info.json (file)](./#info.json)
  * themes (folder)

The following shows a Element Dev Pack containing multiple themes and components:

* MyElementPack.elementsdevpack (bundle)
* info.json
* components (folder)
  * com.companyname.slideshow (folder)
  * com.companyname.navbar (folder)
* themes (folder)
  * com.companyname.themes.architect (folder)
  * com.companyname.themes.solar (folder)

### info.json

The info.json file at the root of your Element Pack defines a few importan things,

```json
{
  "title": "Pack Name",
  "identifier": "com.companyname.packname",
  "author": "Realmac Software",
  "build": "100",
  "version": "1.0.0"
}
```

