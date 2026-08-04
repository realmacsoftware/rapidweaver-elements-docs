---
description: Display responsive resource, custom, or CMS images
---

# Image

The Image component displays a project resource, custom URL, or CMS image. It supports separate light and dark images, responsive framing, lazy loading, fetch priority, an SVG mask, links, and an optional full-screen lightbox.

{% embed url="https://youtu.be/tB5oOctRItM" %}

### Supported Content and File Types

Use Image for bitmap resources such as JPG and PNG. Use the [SVG component](svg.md) when the vector artwork itself needs fill or stroke styling.

### How to Use Image

You’ll find Image under **Media** in the Components list.

1. Drag **Image** onto the page.
2. Choose Resource, Custom, or CMS.
3. Select or enter both Light and Dark sources if needed.
4. Add alternative text or complete the image metadata in Resources.
5. Configure file sizing, loading, aspect ratio, and optional lightbox or mask.

### Component Settings

#### Image

**Type**

* **Resource** — Uses an image stored in the project. This is the default.
* **Custom** — Uses an absolute URL or site-relative path.
* **CMS** — Uses a CMS field expression.

**Mode** switches between Light and Dark while choosing the source. Light is selected by default.

The dark image is shown automatically when the visitor’s browser or operating system is set to dark mode (`prefers-color-scheme: dark`). If no dark image is set, the light image is used everywhere.

Custom mode displays **Source**. CMS mode displays **Field**, which defaults to `{{item.image.src}}`. Both modes provide **Alt** text.

{% hint style="info" %}
CMS images show a placeholder while editing. Preview or publish the page to see the resolved CMS image.
{% endhint %}

For Custom and CMS sources, **Width** and **Height** define the intrinsic image size and default to 1280 × 720. Display size is controlled separately under Sizing.

For Resource images:

* **Original** — Exports the original resource size. This is the default behaviour.
* **Custom** — Exports a resized file. File Size defaults to 400 pixels.

{% hint style="warning" %}
Custom-sized resources are exported at twice the entered width for Retina displays. A File Size of 400 pixels creates an 800-pixel export.
{% endhint %}

**Image Protection** discourages simple right-click downloading and is off by default. It cannot prevent visitors from retrieving an image already delivered to their browser.

**Lazy Loading** adds the browser’s `loading="lazy"` attribute and is off by default. Avoid lazy loading a prominent image near the top of the page.

**Fetch Priority** offers Auto, High, or Low and defaults to Auto.

{% hint style="success" %}
Optimised image dimensions and appropriate lazy loading can improve page performance without reducing visible quality.
{% endhint %}

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-01 at 11 .41.03@2x.png" alt="Image Inspector controls for source, sizing, protection, lazy loading, and fetch priority"><figcaption><p>The Image group controls the source file and loading behaviour.</p></figcaption></figure>

#### Mask

**SVG** selects the mask resource. Black or opaque areas reveal the image.

**Size** offers Contain, Cover, or Fill and defaults to Contain.

#### Lightbox

**Enable** opens the image full-screen when clicked and is off by default.

When enabled, **Color** defaults to Black, **Opacity** to 50%, and **Blur** to 0 pixels.

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-01 at 4 .10.27@2x.png" alt="Image Lightbox controls for backdrop colour, opacity, and blur"><figcaption><p>Lightbox backdrop controls.</p></figcaption></figure>

#### Link

Set **To** to link the image. Avoid enabling both a Link and Lightbox because visitors need one clear click action.

#### Aspect Ratio

**Aspect Ratio**

* **Auto** — Uses the image’s natural ratio. This is the default.
* **Wide** — Uses 16:9.
* **Tall** — Uses 4:5.
* **Custom** — Uses an `x/y` value; the default is `7/5`.

When the ratio is not Auto, **Object Fit** offers Fill, Contain, Cover, None, or Scale Down and defaults to Cover, and **Position** chooses the focal point from the centre, edges, or corners and defaults to Centre.

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-01 at 4 .20.38@2x.png" alt="Image Aspect Ratio controls with object fit and position options"><figcaption><p>Aspect Ratio controls the image frame and crop.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-01 at 4 .19.01@2x.png" alt="Image Inspector showing custom aspect-ratio settings"><figcaption><p>A custom aspect ratio can use any valid x/y value.</p></figcaption></figure>

### A Note About Image Protection

Browsers must download images before displaying them, so no front-end setting can make an image impossible to retrieve. Image Protection only discourages casual saving. Watermark valuable images and export them at an appropriate web resolution.

### Accessibility

Describe informative images with concise alternative text. Leave alt text empty only for purely decorative images, and avoid repeating an adjacent caption word for word.

### Related Components

* [Gallery](gallery.md) — Displays a folder of media in a grid and lightbox.
* [SVG](svg.md) — Displays and recolours vector artwork.
* [Mask](mask.md) — Provides more advanced masking options for wrapped content.

{% include "../../.gitbook/includes/common-controls.md" %}
