---
description: Add Scalable Vector Graphics to your website
---

# SVG

SVGs (Scalable Vector Graphics) have become a go-to choice for web design because they offer incredible flexibility and quality. Unlike traditional image formats like JPEG or PNG, SVGs are vector-based, meaning they’re made up of lines and shapes rather than pixels. This makes them infinitely scalable without losing quality, so they look sharp on any screen size or resolution, from small mobile devices to large desktop monitors.

### Here are a few reasons why SVGs are especially useful on websites:

1\. Crisp at Any Size: SVGs maintain perfect clarity when resized, ensuring icons, logos, and illustrations always appear sharp and professional.

2\. Small File Size: SVGs are typically smaller than high-resolution images, which helps websites load faster. Their code-based structure allows them to be easily optimized, minimizing file size and improving performance.

3\. Easy to Style: SVGs can be styled directly with CSS, making them easy to fit in with the colours and style of your website.

## SVG Controls

### SVG

To add an SVG, drop it from the Finder (or Resources) area into the Dropwell.

### Fill

To set a fill colour on an SVG it needs to be setup correctly to support fill colours.

<table><thead><tr><th width="136">Link Types</th><th>Description</th></tr></thead><tbody><tr><td>None</td><td>No colour or classes will be applied to the SVG.</td></tr><tr><td>Static</td><td>Set a single fill colour on the SVG.</td></tr><tr><td>Hover</td><td>Set a Start and End colour for the SVG. The Hover colour is displayed when the mouse cursor is over the SVG.</td></tr></tbody></table>

### Stroke

To set a stroke colour on an SVG it needs to be setup correctly to support stroke colours.

<table><thead><tr><th width="136">Link Types</th><th>Description</th></tr></thead><tbody><tr><td>None</td><td>No colour or classes will be applied to the SVG.</td></tr><tr><td>Static</td><td>Set a single fill colour on the SVG.</td></tr><tr><td>Hover</td><td>Set a Start and End colour for the SVG. The Hover colour is displayed when the mouse cursor is over the SVG.</td></tr><tr><td>Width</td><td>Set a stroke width for the SVG in pixels.</td></tr></tbody></table>

### Q\&A on fixing SVG's for display on a website.

Getting SVG's to display correctly is a bit of a dark art, but with a bit of tinkering you'll be able to modify them to work and look great on the web and in Elements.

#### Q: Why doesn't the Fill or Stroke colour work as expected?

SVG images don’t always respond as expected to CSS styles for a few reasons, and it’s a common stumbling block. Here’s a quick rundown on why this happens and how to get more reliable control over your SVGs in RapidWeaver Elements…

SVG elements have their own styling properties, like fill and stroke, which can sometimes conflict with CSS styles. If these attributes are set within the SVG code itself (e.g., ), they can override CSS. For greater flexibility, try removing these inline attributes and letting CSS handle the styling.

For scalable, theme-compatible SVGs, you can set the fill and stroke attributes to currentColor within the SVG file. This approach allows Elements to set SVG color for the stroke or Fill.

Set `fill="currentColor"` within your SVGs if you want Elements to set the colour of the stroke or fill.

#### Q: How do I change the size of an SVG?

A: Use the Sizing settings in the component inspector, by default this is set to use a Theme Studio value. [Custom CSS values](../custom-css-values.md) can also be used to size the SVG.

#### Q: Why doesn't the SVG change size when I adjust the sizing in Elements?

A: Remove the height and width values in the SVG file, see screenshot below for an example.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-23 at 11 .32.29@2x.png" alt=""><figcaption></figcaption></figure>

#### Q: Where can I find SVG Icons for use in Elements?

A: [Tabler Icons](https://tabler.io/icons) has over 5,650 free SVG icons, they are all perfect for use on your Elements websites. Download any of the icons from there and remove the width and height code (as above), and they are ready to use in your project. The icons from Tabler are setup to use the stroke attribute. See the video below for a quick overview of how this works in practice.

{% embed url="https://share.cleanshot.com/TsQRDhMX" %}

### Free SVG Icon Libraries

All of the following icon libraries work well Elements, if you require them to be resiable in Elements you'll need to remove the Height and Width values from the code before importing.

* [https://tabler.io/icons](https://tabler.io/icons), over 5,650 free SVG icons.
* [https://feathericons.com](https://feathericons.com), simply beautiful open source icons
* [https://phosphoricons.com](https://phosphoricons.com/?size=64\&weight=%22duotone%22), outline, filled, duotone and more.

### Further Reading

* [Practical SVG](https://practical-svg.chriscoyier.net) by Chris Coyier

