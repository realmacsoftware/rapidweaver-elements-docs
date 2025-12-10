---
description: Configure fonts for use in your website
---

# Font Family

Font families define the overall personality of your site, and Elements gives you three straightforward ways to configure them. You can stick with fast, reliable system fonts, load your own custom font files, or pull from Google Fonts.&#x20;

This page walks you through each option, how they differ, and when to use them so you can get the look you want without any headaches.

### Using System Fonts

Webfonts were great when most computers only had a handful of good fonts pre-installed. Thanks to font creation and buying by Apple, Microsoft, Google, and other folks, most computers have good—no, great—fonts installed, and they're a great option if you want to _not_ load a separate font.

Learn more about what fonts are supported by popular operating systems on the following sites:

* [https://systemfontstack.com](https://systemfontstack.com)
* [https://modernfontstacks.com](https://modernfontstacks.com)

### Using Custom Fonts

Elements includes a built-in Font Manager that lets you add your own local web fonts. It supports common formats like .woff, .woff2, and .ttf, making it easy to use custom typography in your designs.

Watch the video below to learn more about adding custom fonts to your website:

{% embed url="https://youtu.be/KdEVDwbr4JU" %}

For best browser support and performance, custom fonts should be provided in WOFF2 format. **WOFF** (the **Web Open Font Format**) is a web font format developed by Mozilla, Type Supply, LettError, and other organisations.

#### Recommended formats (in order of preference):

1. WOFF2 – Most modern and efficient format (used by all modern browsers).
2. WOFF - Good option when also supporting older browsers.
3. TTF - Mostly for legacy or specific use cases (not recommended for production due to larger size and weaker compression).

{% stepper %}
{% step %}
#### Add a Fonts Folder to Your Project

1. Open your project in Elements.
2. Go to Resources.
3. Create a new folder named "fonts" (lowercase is recommended).
4. Drag your downloaded font files into this folder.
   * A font may contain a single face or multiple weights.

<figure><img src="../../.gitbook/assets/CleanShot 2025-05-05 at 7 .22.28@2x.png" alt=""><figcaption></figcaption></figure>


{% endstep %}

{% step %}
#### Create a Custom Font in Theme Studio

1. Open Theme Studio.
2. In the Font Family section, add a New Custom Font.
3. Give it a name, like Mighty or Rubik.
4. Set Kind to Font Resource.
5. Drag your font files from Resources into the drop area.
   * For a single-face font, drag in the one file.
   * For multi-weight fonts, add each weight file.&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2025-05-05 at 7 .18.20@2x.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/CleanShot 2025-05-05 at 7 .23.21.gif" alt=""><figcaption></figcaption></figure>


{% endstep %}

{% step %}
#### Assign Weights for Multi-Font Families

Elements usually detects weights correctly, but it depends on how the font is packaged.

1. Select each imported font file.
2. Check the assigned Weight in the Inspector.
3. Correct anything that isn’t right. This ensures Elements uses the proper weights when you switch between font styles.
{% endstep %}

{% step %}
#### Apply the Custom Font to Elements in Your Project

1. Select a text component.
2. Change its Font to your new custom font. The change appears immediately.&#x20;
{% endstep %}
{% endstepper %}

### Troubleshooting

If a custom font doesn’t appear correctly:

* Check the weight assignments in the Inspector.
* Make sure the fonts are placed in the fonts folder inside Resources.
* Re-add the font in Theme Studio if needed.

If you still have trouble, visit the [Elements Forum](https://forums.realmacsoftware.com/), we’re always happy to help.&#x20;
