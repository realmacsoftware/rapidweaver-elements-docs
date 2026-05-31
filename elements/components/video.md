---
description: Add video to your webpage
---

# Video

The Video Element lets you drop a single video into any part of your site with no fuss. It handles YouTube, Vimeo, and standard video files, giving you a clean, reliable way to showcase clips whether they’re hosted online or stored locally. This makes it ideal for product demos, hero sections, tutorials, and anything else where a focused video presentation matters.

{% embed url="https://youtu.be/avzBCXIJFU0" %}

### Adding Video to your Projects

You can add a video in a few different ways. For YouTube or Vimeo, drag the video URL from your browser straight into the Resources area. If you have a local video file, drag it in from the Finder and Elements will add a copy to your project. You can also import a video from any remote URL.

{% hint style="success" %}
Video can be added to the **background of your site** by using the Container Component.\
Watch this video to learn more: [How to add a background video header to your webpage](https://youtu.be/x59UfuZvMwM)
{% endhint %}

#### Supported Video Types

The video component supports the following file types:

* YouTube
* Vimeo
* .mp4

#### Dropzone

The Video component has a drop-zone in the center of it to allow for custom play buttons, text, graphics, and more.

### Video Component Settings

{% columns %}
{% column width="50%" %}
#### Video

You can add video in several ways. Drag a YouTube or Vimeo URL straight into Resources, drag in a local file from the Finder, or import a video from any remote URL.

**Resource**\
These settings define the source and play details for your video.

**Options**\
Set when (or if) the video should play automatically.

*   **Autoplay**

    The following options are available: Immediately, When in Viewport, or Never.
*   **Muted**

    Set the video to muted by default.
* **Controls**\
  Hide or show the video player controls. This setting only works with .mp4 files.
* **Loop**\
  Specify if the video should loop. This setting only works with .mp4 files.
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../../.gitbook/assets/CleanShot 2025-11-17 at 10 .40.54 2@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column width="50%" %}
#### Lightbox

The Lightbox allows the video to open in an overlay when clicked, giving it full focus without leaving the page.

**Enable**\
These settings control how the lightbox appears behind the video.

*   **Color**

    Sets the backdrop colour shown behind the video while the lightbox is open.
* **Opacity**\
  Adjusts how transparent the backdrop is. Higher values create a darker, more solid overlay.
* **Blur**\
  Adds a subtle blur effect to the page behind the video.
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../../.gitbook/assets/CleanShot 2025-11-17 at 10 .45.09@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column width="50%" %}
#### Thumbnail

Thumbnail lets you set the image shown before the video plays. It’s ideal for controlling the look of the video before it loads and helps create a clean, intentional layout.

{% hint style="success" %}
If you’re using a YouTube link, Elements automatically pulls in the video’s thumbnail and uses it as the default image.
{% endhint %}

* **Type**\
  Choose between Resource, Custom, or CMS to determine how the image is loaded.
* **Mode**\
  Choose separate thumbnail images for Light Mode and Dark Mode so the design looks correct in both themes.
* **Image**\
  Select the image that appears as the thumbnail. Use a jpg file for best performance and visual quality.
* **Alt**\
  Sets the alt text for the thumbnail image. This improves accessibility and helps search engines understand the content.
* **Overlay**\
  Adds a colour overlay to the thumbnail. Useful for dimming the image and making the play button stand out.
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../../.gitbook/assets/CleanShot 2025-11-17 at 10 .48.49@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
#### Aspect Ratio

The Aspect Ratio section controls the shape and framing of the video thumbnail. You can use predefined ratios for quick layouts or set a custom ratio for more precise control.

Additional options let you control how the image fits and where it’s positioned within its frame.

{% hint style="warning" %}
The aspect ratio applies to the Thumbnail and not the video.
{% endhint %}

**Aspect Ratio**\
These settings define the overall shape of your image container. Choose from Auto, Wide, or Tall presets to control how the image is displayed.

* Auto: Adapts to the image’s original dimensions.
* Wide: Creates a landscape-style frame.
* Tall: Creates a portrait-style frame.
* Custom: More control over cropping.

The **Custom Ratio** allows you to define a specific aspect ratio manually. Enter a ratio in the format x/y, such as 1/1 for a square or 5/7 for portrait-style content.

**Object Fit**\
Determines how the image is scaled within its container.

* **Fill**: Stretches the image to fill the container, possibly distorting it.
* **Contain**: Ensures the full image is visible within the container.
* **Cover**: Crops edges if necessary to fill the container without distortion.
* **None**: Keeps the image at its original size.
* **Scale Down**: Reduces the image size only if it’s larger than the container.

**Position**\
Controls where the image is anchored within its container. Choose from positions like: Top, Center, Bottom, Left, Right, or combinations like Top Center, Bottom Right, etc.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/CleanShot 2025-11-01 at 4 .20.38@2x.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-01 at 4 .19.01@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% include "../../.gitbook/includes/common-controls (1).md" %}
