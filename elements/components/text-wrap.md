---
description: Flow text around a transparent or rectangular image
---

# Text Wrap

Text Wrap places an image to the left or right of its child content so text flows around it. With a transparent PNG, WebP, or SVG, the text can follow the visible shape instead of the image’s rectangular bounds.

{% hint style="info" %}
Text Wrap supports image resources, custom image URLs, and CMS image fields.
{% endhint %}

### How to Use Text Wrap

You’ll find Text Wrap under **Layout** in the Components list.

1. Drag **Text Wrap** onto the page.
2. Place one or more Text or Typography components inside it.
3. In **Media**, choose Resource, Custom, or CMS and provide the image.
4. Add alternative text.
5. Choose Left or Right under Float, then adjust Width, Margin, and Threshold.

<figure><img src="../../.gitbook/assets/CleanShot 2026-07-15 at 10 .43.06@2x.png" alt="A Text Wrap component containing text with an image floated beside it"><figcaption><p>A basic Text Wrap setup in Elements.</p></figcaption></figure>

### Component Settings

#### Media

**Type**

* **Resource** — Uses an image from the project. This is the default.
* **Custom** — Uses a URL or path entered in Source.
* **CMS** — Uses a CMS field. The default field is `{{item.image.src}}`.

**Alt Text** describes the image for search engines and assistive technologies. Leave it empty only when the image is purely decorative.

**Float**

* **None** — Displays the image without floating text around it.
* **Left** — Floats the image to the left. This is the default.
* **Right** — Floats the image to the right.

**Width** sets the image width and defaults to 40%.

**Margin** controls the space between the image and text and defaults to theme spacing 4.

**Threshold** controls how opaque a pixel must be before text stops wrapping. It defaults to 50%. Lower values keep text farther from soft or translucent edges.

### Accessibility

Add useful alternative text when the image conveys information. Keep line lengths readable around the shape and check that narrow screens do not leave an uncomfortably small text column.

### Tips and Best Practices

* **Use transparent assets for shaped wrapping:** A solid image wraps text around its full rectangle.
* **Use longer copy:** The effect is most useful when there is enough text to flow below the image.
* **Check mobile widths:** Reduce the image width or disable Float when the remaining text column becomes too narrow.

### Related Components

* [Image](image.md) — Displays a standalone image with lightbox and sizing controls.
* [Typography](typography.md) — Provides a styled long-form content block to wrap around the image.

{% include "../../.gitbook/includes/common-controls.md" %}
