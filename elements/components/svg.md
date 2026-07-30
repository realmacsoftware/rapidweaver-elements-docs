---
description: Display and style scalable vector graphics
---

# SVG

The SVG component displays scalable vector artwork such as icons, logos, and illustrations. SVGs remain sharp at every size and can often be recoloured directly from Elements.

{% hint style="info" %}
By default, the component removes size, fill, stroke, and style attributes from the rendered SVG so its appearance can be controlled in the Inspector. The original resource stored in Elements is not changed.
{% endhint %}

### Supported Content and File Types

The component accepts SVG resources. Use the [Image](image.md) component for JPG, PNG, and other bitmap images.

### How to Use SVG

You’ll find SVG under **Media** in the Components list.

1. Drag **SVG** onto the page.
2. Drop an SVG from Finder or Resources into the SVG field.
3. Decide which embedded attributes Elements should remove.
4. Configure Fill, Stroke, Link, and Sizing.
5. Preview hover states in a browser.

### Component Settings

#### SVG

**SVG** selects the resource.

Under **Remove Attributes**, each switch controls whether Elements strips that attribute while rendering:

* **Size** — Removes embedded width and height. Enabled by default.
* **Fill** — Removes embedded fill attributes. Enabled by default.
* **Stroke** — Removes embedded stroke attributes. Enabled by default.
* **Styles** — Removes embedded style attributes. Enabled by default.

Disable a switch when the original SVG must retain that attribute.

#### Fill

**Type** can be None, Static, or Hover.

For Hover, **Over** chooses Self or Parent and **State** switches between Start and End.

Each visible state provides **Color** and **Opacity**. Both Start and End default to Surface 50 at 100% opacity.

#### Stroke

**Type** can be None, Static, or Hover. Hover provides Start and End states and can be triggered by Self or Parent.

Each state provides **Color**, **Opacity**, and **Width**. Colours default to Surface 50, opacity to 100%, and width to 1.

#### Link

Set **To** to make the SVG link to a page, resource, website, email address, phone number, anchor, or another supported destination.

### Preparing SVG Files

Elements can remove common attributes at render time, but the SVG’s internal structure still determines whether fills and strokes respond correctly.

* Remove fixed `width` and `height` values when the SVG does not resize as expected.
* Use `currentColor` for fill or stroke when the artwork is designed to inherit a colour.
* If `currentColor` prevents the Inspector from controlling the artwork, remove it and test again.
* Complex inline styles or multiple hard-coded fills may require editing in an SVG tool.

<figure><img src="../../.gitbook/assets/CleanShot 2024-11-12 at 10 .34.54@2x.png" alt="SVG code showing a fill attribute set to currentColor"><figcaption><p>Use currentColor—or remove a fixed fill—when the SVG should inherit its colour.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/CleanShot 2024-10-23 at 11 .32.29@2x.png" alt="SVG code with fixed width and height attributes highlighted for removal"><figcaption><p>Remove fixed width and height values when they prevent responsive sizing.</p></figcaption></figure>

For a practical workflow, see [SVG Cleanup with Sketch](https://forums.realmacsoftware.com/t/svg-cleanup-with-sketch-app/46751). You can use [Sketch](https://www.sketch.com) with the [SVGO Compressor plugin](https://sketchelements.com/plugins/svgo-compressor/).

{% embed url="https://share.cleanshot.com/TsQRDhMX" %}

### Free SVG Icon Libraries

* [Lucide](https://lucide.dev)
* [Tabler Icons](https://tabler.io/icons)
* [Feather Icons](https://feathericons.com)
* [Phosphor Icons](https://phosphoricons.com/)
* [SVGL](https://svgl.app)
* [Heroicons](https://heroicons.com/outline)
* [Google Material Symbols](https://fonts.google.com/icons)
* [Logoipsum](https://logoipsum.com/)

For a deeper introduction to working with SVG, see [Practical SVG](https://practical-svg.chriscoyier.net).

### Accessibility

Decorative SVGs should not duplicate nearby text. When an SVG conveys meaning, provide an accessible text label through the surrounding link, button, caption, or content structure.

### Troubleshooting

#### Fill or stroke does not change

Check for hard-coded fill, stroke, class, or style values inside the SVG. Enable the relevant Remove Attributes switches, or clean the file in an SVG editor.

#### The SVG does not resize

Enable **Remove Attributes → Size** or remove fixed width and height attributes from the source SVG, then use the component’s Sizing controls.

### Related Components

* [Image](image.md) — Displays bitmap images with responsive source and lightbox controls.
* [Mask](mask.md) — Uses an SVG to reveal wrapped content.

{% include "../../.gitbook/includes/common-controls.md" %}
