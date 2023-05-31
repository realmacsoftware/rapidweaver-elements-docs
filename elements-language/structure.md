---
description: An Element is a bundled folder
---

# Bundle Structure

Elements require a specific directory structure in order to work correctly, these are called Bundles in macOS.

Element bundles are directory hierarchies, with the top-level directory having a name that ends with a `.rwdevpack` or `.rwelementpack` extension.

### Distributing Element Packs

RapidWeaver Element Packs (.rwelementpack) are highly optimised encrypted bundles compiled from an RapidWeaver Dev Pack (.rwdevpack) and ready for distribution.&#x20;

RapidWeaver Dev Packs are only for development and should not be distributed.

Elements should only be distributed as compiled RapidWeaver Element Packs (.rwelementpack).

### Dev Element Bundle Structure

The following outlines the folder structure supported by elements — Only **bold items are required** for a basic Element to function inside of RapidWeaver.

{% hint style="info" %}
An Element pack can contain multiple Elements, each Element should be placed in the "elements" folder inside the main bundle.
{% endhint %}

* **HelloWorld.rwdevpack** (bundle)
  * **elements** (folder)
    * **com.realmac.elementpack.helloworld** (folder)
      * hooks.js
      * **icon.icns**
      * **info.json**
      * properties.json
      * **templates** (folder)
        * **each** (folder)
          * **index.html**
          * styles.css
        * include (folder)
          * extra.html
        * page (folder)
          * page.html

Here's a Finder window showing the above Element layout on macOS Ventura.

<figure><img src="../.gitbook/assets/CleanShot 2023-05-31 at 14.08.03@2x.png" alt=""><figcaption><p>Finder window showing the layout of a typical Element.</p></figcaption></figure>

And the same Element being edited in [Visual Studio Code](https://code.visualstudio.com).

<figure><img src="../.gitbook/assets/CleanShot 2023-05-31 at 14.26.45@2x.png" alt=""><figcaption><p>Editing an Element in Visual Studio Code</p></figcaption></figure>
