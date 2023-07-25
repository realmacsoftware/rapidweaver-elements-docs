# Icons

At a bare minumim you'll want to include an "icon.icns" file, this icns file can be used for all views where your Element appears within the RapidWeaver Elements UI.

{% hint style="info" %}
We recommend [Icon Slate](https://www.kodlian.com/apps/icon-slate) to compile .icns files.
{% endhint %}

Your main icon.icns file should be named in the Elements info.plist.&#x20;

* **icon.icns (Required)**
* icon-dark.icns (optional)
* paletteIcon.png (optional)
* paletteIcon-dark.png (optional)

Supported image sizes in the icon.icns file.

* 16x16.png / 16x16@2x.png
* 32x32.png / 32x32@2x.png
* 128x128.png / 128x128@2x.png
* 256x256.png / 256x256@2x.png (optional)
* 512x512.png / 512x512@2x.png (optional)

Supported image size/ratio for the Palette Icon.

* 128x256
* 128x256@2x

### Asset Placement

Icon files should be placed at the root of the Element alongside the info.json file.

<figure><img src="../../.gitbook/assets/CleanShot 2023-07-25 at 4.14.41@2x.png" alt=""><figcaption><p>Finder window showing the icon files inside of a typical Element.</p></figcaption></figure>
