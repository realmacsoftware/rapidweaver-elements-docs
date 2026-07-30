---
description: Build a responsive image and video gallery with a lightbox
---

# Gallery

The Gallery component turns a Resources folder into a responsive media grid with optional captions, author information, and a full-screen lightbox. It can combine images, YouTube and Vimeo links, and MP4 video.

{% embed url="https://youtu.be/LwmA-IZNQIs" %}

{% hint style="success" %}
Add a YouTube or Vimeo video by dragging its URL from your browser into Resources. Playlist URLs can also be added.
{% endhint %}

### Supported Content and File Types

* JPG
* PNG
* YouTube
* Vimeo
* MP4

The Gallery expects a folder rather than a single image.

### How to Use Gallery

You’ll find Gallery under **Media** in the Components list.

1. Create a folder in Resources and add the images or videos.
2. Drag **Gallery** onto the page.
3. Drop the Resources folder into **Media → Resources**.
4. Set the column count, gap, and thumbnail ratio.
5. Configure thumbnail metadata and lightbox styling.
6. Preview images and videos in a browser.

{% hint style="info" %}
For sharp modern displays, use gallery images at least 1200 pixels wide. [Squash for macOS](https://www.realmacsoftware.com/squash/) can batch resize and compress them.
{% endhint %}

### Component Settings

#### Media

**Resources** selects the folder containing gallery media.

<figure><img src="../../.gitbook/assets/CleanShot 2025-10-16 at 11 .45.57@2x.png" alt="The Gallery Media settings with a Resources folder selected"><figcaption><p>The Gallery is built from a folder in Resources.</p></figcaption></figure>

#### Layout

**Columns** sets between 1 and 12 columns and defaults to 3.

**Gap** sets spacing between thumbnails and defaults to theme spacing 3.

<figure><img src="../../.gitbook/assets/CleanShot 2025-10-16 at 11 .50.41@2x.png" alt="Gallery Layout settings showing Columns and Gap controls"><figcaption><p>Layout controls the number and spacing of gallery columns.</p></figcaption></figure>

#### Thumbnails

**Media**

* **Aspect** — Square, Wide, or Tall. Square is the default and applies to every thumbnail.
* **Radius** — Sets thumbnail corner rounding.
* **Shadow** — Applies a theme shadow.

**Meta Data**

* **Alignment** — Left, Centre, or Right. Left is the default.
* **Margin** — Space above metadata; defaults to 0.
* **Spacing** — Space between metadata items; defaults to 0.

**Caption** and **Author** are hidden by default. Enabling either reveals Color, Font, and Size. Both default to Text 50, the Heading font, and Small size.

{% hint style="warning" %}
One Aspect applies to the complete gallery. Use a custom Grid layout when mixed thumbnail ratios must remain visible.
{% endhint %}

<figure><img src="../../.gitbook/assets/CleanShot 2025-10-16 at 11 .52.29@2x.png" alt="Gallery Thumbnails settings for aspect, metadata, caption, and author styling"><figcaption><p>Thumbnail media and metadata can be styled independently.</p></figcaption></figure>

#### Lightbox

**Preview** opens the lightbox in Edit mode and is off by default.

**Media** has separate Radius and Shadow controls for the enlarged media.

**Meta Data** controls Alignment, Margin, and Spacing below the lightbox media. Alignment defaults to Centre, Margin to theme spacing 3, and Spacing to 0.

Caption and Author are hidden by default and each provides Color, Font, and Size when enabled.

<figure><img src="../../.gitbook/assets/CleanShot 2025-10-16 at 12 .01.49@2x.png" alt="Gallery Lightbox settings for media and metadata"><figcaption><p>The lightbox can use different media and metadata styling from the grid.</p></figcaption></figure>

#### Overlay

**Color** sets the page backdrop and defaults to Surface 50.

**Opacity** defaults to 20%.

**Blur** defaults to 3 pixels.

<figure><img src="../../.gitbook/assets/CleanShot 2025-10-16 at 12 .05.07@2x.png" alt="Gallery Overlay controls for colour, opacity, and blur"><figcaption><p>Overlay settings draw attention to the selected media.</p></figcaption></figure>

#### Navigation

General controls set **Border Radius**, **Padding**, and icon **Size** for navigation buttons. Defaults are Full radius, theme spacing 2, and 24 pixels.

Use **State** to switch between Default and Hover styling.

**Close Button** and **Next & Previous Buttons** each provide Background, Icon, and Opacity for both states. Default opacity is 100%.

<figure><img src="../../.gitbook/assets/CleanShot 2025-10-16 at 1 .07.09@2x.png" alt="Gallery Navigation controls for close, next, and previous buttons"><figcaption><p>Navigation buttons have independent Default and Hover styles.</p></figcaption></figure>

### Accessibility

Add meaningful captions or image metadata when media conveys information. Keep lightbox controls high contrast, and make sure videos remain usable with keyboard controls.

### Tips and Best Practices

* **Optimise before importing:** Smaller files improve loading and lightbox performance.
* **Use consistent crops:** A shared thumbnail ratio makes the grid feel intentional.
* **Keep controls visible:** Test navigation colours over both light and dark media.

### Related Components

* [Image](image.md) — Displays one image with optional lightbox.
* [Image Slider](image-slider.md) — Presents images in a swipeable carousel.
* [Grid](grid.md) — Builds a fully custom media layout.
