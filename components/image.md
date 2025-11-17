---
description: Add images to your webpage
---

# Image

The Image component in Elements allows you to easily add and display images (in JPG or PNG formats) on your website. This versatile component supports a wide range of customisation options, making it ideal for showcasing images in a clean, responsive, and accessible way.

{% embed url="https://youtu.be/tB5oOctRItM" %}

### Supported Image Types

* JPG
* PNG

The Image Component does not support SVG's, instead you should use the [SVG Component](svg.md).

### Image Component Settings

{% columns %}
{% column width="50%" %}
#### Image

The Image control lets you add and manage images within your Project. You can select an image from project resources, link a custom URL, or connect a CMS image.

{% hint style="success" %}
**Tip:** Using optimised image sizes and lazy loading can significantly improve page performance without sacrificing visual quality.
{% endhint %}

**Resource**\
These settings define the source and accessibility details for your image.

* **Type**\
  Choose between Resource, Custom, or CMS to determine how the image is loaded.
* **Mode**\
  Switch between Light and Dark mode images to display different visuals depending on the users system setting.
* **Image**\
  Use Choose… to select an image from the Finder or Clear to remove the current one. You can also drag and drop in images from the Resources panel or the Finder.
* **Alt**\
  Defines the alternative text used for SEO and accessibility purposes.

**Sizing**\
These options control how the image is scaled.

*   **Type**

    Select Original to display the image at full resolution, or Custom to set a specific width.
*   **File Size**

    Enter a pixel value to define the physical image width when Custom sizing is active.

{% hint style="warning" %}
Resized images are exported at 2x to ensure they look crisp on retina displays. So if you set File size to 400px, it will actually be exported at 800px.&#x20;
{% endhint %}

**Image Protection**\
Prevents visitors from easily downloading the image. However, this is not foolproof, [see note below](image.md#a-short-note-about-why-image-protection-isnt-foolproof-on-the-web).

*   **Enable**

    Disables right-click saving and other common download actions.

**Lazy Loading**\
Improves page performance by deferring image loading until it’s visible in the viewport.

*   **Enable**

    Adds the loading="lazy" attribute to the image tag.

**Fetch Priority**\
Controls how the browser prioritises loading this image.

* **Auto**\
  Uses the browser’s default priority.
* **High**\
  Prioritises loading this image sooner.
* **Low**\
  Defers loading until other elements have finished.
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../.gitbook/assets/CleanShot 2025-11-01 at 11 .41.03@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

#### A short note about Why “Image Protection” Isn’t Foolproof on the Web

It’s a common request: protect images on a website from being downloaded or copied. While blocking right-click can deter casual users, it’s important to understand that it doesn’t truly secure your images. Web browsers inherently download all page assets—including images—so they can display them. This means anyone with basic knowledge of developer tools or access to the browser’s cache can still retrieve your images.

Instead of relying on “image protection,” consider watermarking your images or ensuring they’re resized and optimised for the web. This approach makes them less valuable for unauthorised use while still serving their purpose on your site.



{% columns %}
{% column %}
#### Lightbox

The Lightbox section lets you display an image in a pop-up overlay when clicked. This creates an immersive, distraction-free viewing experience without leaving the page. You can enable or disable the Lightbox and adjust the appearance of its backdrop for a polished presentation.

{% hint style="success" %}
**Tip:** For a fully customised Lightbox use the Modal Component and manually build it to your exact specifications.
{% endhint %}

**Settings**\
These controls define how the Lightbox behaves and how its backdrop looks.

*   Enable

    Turns the Lightbox feature on or off. When enabled, clicking the image will open it in a fullscreen overlay.

**Backdrop**\
These options adjust the appearance of the overlay that appears behind the image.

*   **Color**

    Sets the backdrop colour displayed behind the image. Typically a dark colour (such as black) provides the best contrast.
*   **Opacity**

    Controls the transparency of the backdrop colour, expressed as a percentage. Lower values create a lighter overlay, while higher values make it more opaque.
*   **Blur**

    Adds a background blur effect (in pixels) to soften the content behind the image and draw more focus to the Lightbox image itself.
{% endcolumn %}

{% column %}
<figure><img src="../.gitbook/assets/CleanShot 2025-11-01 at 4 .10.27@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



{% columns %}
{% column %}
#### Aspect Ratio

The Aspect Ratio section controls the shape and framing of images and other visual content. You can use predefined ratios for quick layouts or set a custom ratio for more precise control.&#x20;

Additional options let you control how the image fits and where it’s positioned within its frame.

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
<figure><img src="../.gitbook/assets/CleanShot 2025-11-01 at 4 .20.38@2x.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/CleanShot 2025-11-01 at 4 .19.01@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



{% include "../.gitbook/includes/common-controls (1).md" %}
