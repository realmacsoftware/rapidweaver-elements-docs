# Icons

At a bare minimum you'll want to include PDF images for light mode icons so they can be used for all views where your Component appears within the RapidWeaver Elements UI.&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2024-10-18 at 5 .36.55.gif" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Important:** The PDF graphic for your icon should have a transparent background so it can be composited in app on to the background tile to give a constant for Components in Elements.&#x20;
{% endhint %}

### Standard Icon

All Elements require an icon.pdf file for light mode. If the dark-mode.pdf file isn't provided, icon.pdf will be used in Dark Mode.

* **icon.pdf (Required), 1:1 ratio, e.g. 128x128 (Square)**
* icon-dark.pdf (optional), 1:1 ratio, e.g. 128x128 (Square)

### Palette Icons

The Palette image should be named paletteIcon.pdf and paletteIcon-dark.pdf for Dark Mode. If the paletteIcon-dark.pdf file isn't provided, paletteIcon.pdf will be used in Dark Mode.

* **paletteIcon.pdf (Required), 1:2 ratio, e.g. 128x256 (landscape)**
* paletteIcon-dark.pdf (optional), 1:2 ratio, e.g. 128x256 (landscape)

### Sketch Example File

Your pdf icons should be on a transaparent background.

<figure><img src="../../.gitbook/assets/CleanShot 2024-08-21 at 11 .39.38@2x.png" alt=""><figcaption></figcaption></figure>

We've provided an example Sketch document below you can use to get started.

{% file src="../../.gitbook/assets/Components Icon Template.zip" %}

### Asset Placement

All Icon files should be placed at the root of the Component alongside the info.json file.

<figure><img src="../../.gitbook/assets/CleanShot 2024-10-18 at 5 .29.48@2x.png" alt=""><figcaption><p>Finder window showing the icon files inside of a typical Element.</p></figcaption></figure>



***

### Experimental / Unsupported - Banner Icons

{% hint style="info" %}
⚠️ While this feature works, please do not use it as it may be removed in a future build.
{% endhint %}

We also offer experimental support for banner style icons, these are great for layout style components. However, this style of icon may not be supported when Elements ships, please use with caution and ensure you also include the standard style of icon.

* bannerLayer1.png
* bannerLayer1-Dark.png (optional)

Banner icons can be layered, and each layer can represent a different colour in the Theme Studio. For example this icon uses four layers and three of those layers will be tinted with the Theme colour.

* bannerLayer1.png
* bannerLayer2-primary-500.png
* bannerLayer3-primary-200.png
* bannerLayer4-secondary-500.png

Banner images should be 512px in width, but can be as short or tall as you need.

### **List View Icon** (Standard Icon)

<figure><img src="../../.gitbook/assets/CleanShot 2023-08-05 at 10 .46.36@2x (1).png" alt=""><figcaption><p>Element Library: List view icons (Developer Beta 12)</p></figcaption></figure>

### Grid View (Pallete Icon)

<figure><img src="../../.gitbook/assets/CleanShot 2023-08-05 at 10 .46.30@2x.png" alt=""><figcaption><p>Element Library: Grid view icons (Developer Beta 12)</p></figcaption></figure>

### Grid and List View (Banner Icon)

Banner icons will appear the same in both grid and list.

<figure><img src="../../.gitbook/assets/CleanShot 2024-05-12 at 6 .51.51@2x (1).png" alt=""><figcaption><p>Element Library: Grid view icons (Pre-Beta Build 22484)</p></figcaption></figure>



