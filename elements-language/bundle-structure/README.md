---
description: An Element is a bundled folder
---

# Bundle Structure

Elements require a specific directory structure in order to work correctly, these are called Bundles in macOS.

Element bundles are directory hierarchies, with the top-level directory having a name that ends with a `.elementsdevpack` extension.

The Pro version of RapidWeaver Elements is required to build and develop Elements.

### Dev Pack Bundle Structure

The following outlines the folder structure supported by elements — Only **bold items are required** for a basic Element to function inside of RapidWeaver.

{% hint style="info" %}
An Element pack can contain multiple components, each Element should be placed in the "elements" folder inside the main bundle.
{% endhint %}

* **HelloWorld.elementsdevpack** (bundle)
* **components (folder)**
  * **info.json**
  * **com.yourcompany.component.helloworld** (folder)
    * [hooks.js](../hooks.js/)
    * [**icon.icns**](icons.md)
    * icon-dark.icns
    * [**info.json**](info.json.md)
    * paletteIcon.png
    * paletteIcon-dark.png
    * [**properties.json**](../properties.json/)
    * assets (folder)
      * page (folder)
    * **templates (folder)**
      * **index.html**
      * each (folder)
        * index.html
        * styles.css
      * [include](../templates/includes.md) (folder)
        * extra.html
      * page (folder)
        * page.html
  * com.yourcompany.component.foobar (folder)
  * shared (folder)
    * assets (folder)
    * hooks (folder)
    * templates (folder)

### Dev Pack with Multiple Elements

An Element pack can have multiple addons inside of it, including components and themes, here's an example structure:

* yourAddons.elementsdevpack (bundle)
* [info.json](info.json.md)
* components (folder)
  * com.yourcompany..image (folder)
  * com.yourcompany..navbar (folder)
* [themes](../themes.md) (folder)
  * com.yourcompany..themes.architect (folder)
  * com.yourcompany..themes.solar (folder)

