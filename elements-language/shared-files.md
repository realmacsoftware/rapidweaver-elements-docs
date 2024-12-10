---
icon: folder-closed
---

# Shared Files

The shared folder lives at the root of the Element Dev Pack and is accesible by all components in the pack.

* MyElementPack.elementsdevpack (folder/bundle)
  * components (folder)
  * [info.json (file)](shared-files.md#info.json)
  * themes (folder)
  * **shared (folder)**
    * assets (folder)
    * hooks (folder)
    * templates (folder)
      * bodyStart (folder)
      * bodyEnd (folder)
      * headEnd (folder)
      * headStart (folder)

### Assets Folder

Any required asset files can be store here. It might include things like Javascript Files, Fonts, CSS, and Images. To link to a shared asset, you can create an html file in the Templates folder.

The following code would link to an asset called "example-script.js"

```
<script src="{{assetPath}}/example-script.js"></script>
```

<figure><img src="../.gitbook/assets/CleanShot 2024-12-01 at 2 .51.52@2x.png" alt=""><figcaption></figcaption></figure>

### Hooks Folder

This folder can contain all shared hooks.js files. There is no restricion on naming, they just need to be .js files.

{% hint style="info" %}
Shared hook files are compressed into a single file, processed and run first — before individual component hook files.
{% endhint %}

### Templates Folder

This folder can contain extra html templates files, There is no restricion on naming, they just need to be .html files. They should also be stored in one of the following sub folders;

* bodyStart
* bodyEnd
* headEnd
* headStart

{% hint style="info" %}
Shared Template files are only included once in the page per component pack.
{% endhint %}

