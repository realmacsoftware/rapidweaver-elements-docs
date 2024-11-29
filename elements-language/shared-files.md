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

### Assets folder

Any required asset files can be store here. It might include things like Javascript Files, Fonts, CSS, and Images.

### Hooks folder

This folder can contain all shared hooks.js files.

{% hint style="info" %}
**Good to know:** Shared hook files are compressed into a single file, processed and run first — before individual component hook files.
{% endhint %}

### Templates

This folder can contain extra templates files.

{% hint style="info" %}
Shared Template files are only included in the page once per component pack!
{% endhint %}

