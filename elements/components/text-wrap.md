---
description: Effortlessly flow text around images
---

# Text Wrap

**Text Wrap** lets you place images so surrounding copy flows around it, instead of stacking everything in a simple vertical column. Images can be placed to the left or right of the text.

{% hint style="info" %}
The text wrap component supports PNG, WebP, JPG, and SVG image types.
{% endhint %}

### How text wrapping works

Text Wrap uses CSS to float the selected image beside the content. Text flows into the available space around the image.

Use a PNG or WebP with a transparent background. The transparent areas let text follow the visible shape. A solid rectangular image wraps text around its full rectangle.

The component works best with longer text and a modest image width.

### How to use the Text Wrap Component

Start with a **Container** to define the section, add padding to the top, bottom, and sides to give the Text Wrap component a clean section with some breathing room.

Text or Typography Components should be dropped into the Text Wrap component in the Editor, the image for the text to wrap around should be added to the Resource dropzone in the Text Wrap Component settings (not inside the component where the text is)

You can add multiple Text components inside the Text Wrap component, This is useful if you want to break up the text with headings or subheadings.

1. Add the **Text Wrap Component** to the page
2. Place a **Text Component** inside the **Text Wrap Component**
3. Add a png or webp image with a transparent background from the site resources area into the **Text Wrap Component's** Resource dropzone.
4. Adjust the **Margin** until the wrap feels natural, for most cases this is usually between 3 and 5.

<figure><img src="../../.gitbook/assets/CleanShot 2026-07-15 at 10 .43.06@2x.png" alt=""><figcaption><p>Basic Text Wrap setup in Elements</p></figcaption></figure>
