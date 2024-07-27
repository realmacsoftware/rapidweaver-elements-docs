# Icons

{% hint style="info" %}
**WARNING:** This icon document is out of date. The way icons are generated and displayed have been overhauled. Updated icon docs will be available soon!
{% endhint %}

At a bare minumim you'll want to include an "icon.icns" file, this icns file can be used for all views where your Element appears within the RapidWeaver Elements UI. Additional Palette and Banner icon styles are also available.

### Standard Icon

All Elements require this icon.

* **icon.icns (Required)**
* icon-dark.icns (optional)

Supported image sizes in the icon.icns file.

* 16x16.png / 16x16@2x.png
* 32x32.png / 32x32@2x.png
* 128x128.png / 128x128@2x.png
* 256x256.png / 256x256@2x.png (optional)
* 512x512.png / 512x512@2x.png (optional)

{% hint style="info" %}
We recommend [Icon Slate](https://www.kodlian.com/apps/icon-slate) to compile .icns files.
{% endhint %}

### Palette Icons

The Palette image should be named paletteIcon.png and paletteIcon-dark.png if you'd also like to display a different version in dark mode.

* paletteIcon.png
* paletteIcon-dark.png (optional)

Supported palette image sizes.

* 512x256

### Banner Icons

If you're developing an Element that represents a layout we recommend using the Banner style icon.&#x20;

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
