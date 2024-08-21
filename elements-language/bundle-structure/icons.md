# Icons

At a bare minimum you'll want to include  PDF's images for light mode icons so they can be used for all views where your Component appears within the RapidWeaver Elements UI.&#x20;

### Standard Icon

All Elements require this icon.

* **icon.pdf (Required), 1:1 ratio, e.g. 128x128 (Square)**
* icon-dark.pdf (optional), 1:1 ratio, e.g. 128x128 (Square)

### Palette Icons

The Palette image should be named paletteIcon.pdf and paletteIcon-dark.pdf if you'd also like to display a different version in dark mode.

* **paletteIcon.png (Required), 1:2 ratio, e.g. 128x256 (landscape)**
* paletteIcon-dark.png (optional), 1:2 ratio, e.g. 128x256 (landscape)

### Sketch Example File

Your pdf icons should be on a transaparent background.

<figure><img src="../../.gitbook/assets/CleanShot 2024-08-21 at 11 .39.38@2x.png" alt=""><figcaption></figcaption></figure>

We've provided an example Sketch document below you can use to get started.

{% file src="../../.gitbook/assets/Components Icon Template.zip" %}

### Banner Icons (Experimental)

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



### Asset Placement

All Icon files should be placed at the root of the Element alongside the info.json file.

<figure><img src="../../.gitbook/assets/CleanShot 2023-07-25 at 4.14.41@2x.png" alt=""><figcaption><p>Finder window showing the icon files inside of a typical Element.</p></figcaption></figure>
