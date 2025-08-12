---
description: Setup fonts for use in your website
---

# Font Family

Choose between font name, font resources, and Google fonts.

### Using System Fonts

Webfonts were great when most computers only had a handful of good fonts pre-installed. Thanks to font creation and buying by Apple, Microsoft, Google, and other folks, most computers have good—no, great—fonts installed, and they're a great option if you want to _not_ load a separate font.

Learn more about what fonts are supported by popular operating systems on the following sites:

* [https://systemfontstack.com](https://systemfontstack.com)
* [https://modernfontstacks.com](https://modernfontstacks.com)

### Using Custom Fonts

Elements includes a built-in Font Manager that lets you add your own local web fonts. It supports common formats like .woff, .woff2, and .ttf, making it easy to use custom typography in your designs.

For best browser support and performance, custom fonts should be provided in WOFF2 format. **WOFF** (the **Web Open Font Format**) is a web font format developed by Mozilla, Type Supply, LettError, and other organizations.

#### Recommended formats (in order of preference):

1. WOFF2 – Most modern and efficient format (used by all modern browsers).
2. WOFF - Good option when also supporting older browsers.
3. TTF - Mostly for legacy or specific use cases (not recommended for production due to larger size and weaker compression).

#### Adding Custom Fonts&#x20;

Add your font files to the resources area in Elements, use the media inspector to define a weight (and width if required) for each of the font files.

<figure><img src="../../.gitbook/assets/CleanShot 2025-05-05 at 7 .22.28@2x.png" alt=""><figcaption></figcaption></figure>

Add a new Custom Font in the Theme Studio, give it a name, and set the Kind to "Font Resources"

<figure><img src="../../.gitbook/assets/CleanShot 2025-05-05 at 7 .18.20@2x.png" alt=""><figcaption></figcaption></figure>

Next, drag each font file individually from the resources area of your website into the theme studio window.

<figure><img src="../../.gitbook/assets/CleanShot 2025-05-05 at 7 .23.21.gif" alt=""><figcaption></figcaption></figure>
