---
description: Build beautiful image and video galleries
---

# Gallery

The Gallery component in Elements allows you to build beautiful Galleries in a matter of seconds. Simple place the Gallery component into your site and drop on a folder images (or video).

{% embed url="https://youtu.be/LwmA-IZNQIs" %}

{% hint style="success" %}
You can **add YouTube or Vimeo videos** by dragging and dropping the URL from your web browser to the Resources area in RapidWeaver Elements. A playlist URL can also be dropped into the resources area.
{% endhint %}

### Supported File Types

Galleries can contain a mixture of file types, including:

* JPG
* PNG
* YouTube
* Vimeo
* .mp4

### Resize and Compress Images for Best Results

Elements is designed to be flexible with image sizes, but for best results in galleries, we recommend using images that are at least 1200px wide for modern displays. This ensures your gallery looks sharp on all devices.

For batch resizing and compressing images we recommend [Squash for macOS](https://www.realmacsoftware.com/squash/).

### Component Settings

{% columns %}
{% column width="50%" %}
#### Media

Drop a folder of images, videos, YouTube link, or Vimeo links into the dropzone to build your gallery.

{% hint style="danger" %}
The Gallery does not support single images. They must be in a Folder.
{% endhint %}
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../.gitbook/assets/CleanShot 2025-10-16 at 11 .45.57@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



{% columns %}
{% column %}
### Layout

The Layout section controls how your images are arranged within the Gallery component. Use these settings to define the number of columns and the spacing between each thumbnail.

**Columns**

Adjust the number of columns displayed in your gallery.

* Use the slider to set how many columns of thumbnails appear across your layout.
* The gallery automatically adapts to different screen sizes, ensuring images remain evenly spaced and visually balanced.

**Gap**

Set the spacing between gallery items.

* The Gap value defines the amount of space between thumbnails.
* Use smaller values for a tighter grid or larger ones to give each image more breathing room.
* The value corresponds to Tailwind’s spacing scale, so it remains consistent with your theme settings.
{% endcolumn %}

{% column %}
<figure><img src="../.gitbook/assets/CleanShot 2025-10-16 at 11 .50.41@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



{% columns %}
{% column %}
#### Thumbnails

The Thumbnails section controls how images are displayed within the Gallery component. You can adjust the size, shape, and appearance of the thumbnails, along with metadata such as captions and authors.

{% hint style="warning" %}
The Aspect ratio will apply to all images to give the grid an ascetically pleasing and conistant look. If you wish to mix and match aspect ratios, we recommend building a custom Gallery with the Grid Component.
{% endhint %}

**Media**

These settings define the overall appearance of your thumbnails.

*   **Aspect**

    Choose between Square, Wide, or Tall to control the image aspect ratio.
*   **Radius**

    Adjust the corner rounding of your images.
*   **Shadow**

    Adds a soft drop shadow to thumbnails.

**Meta Data**

Use these options to control how meta information (such as captions or authors) is positioned and spaced around the thumbnail.

*   **Alignment**

    Align metadata text to the Left, Center, or Right of each thumbnail.
*   **Margin**

    Adds spacing around the metadata area and the thumbnail.
*   **Spacing**

    Controls the space between individual metadata items (for example, between a caption and author line).

**Caption & Author**

Controls the appearance of the image caption and author

*   **Show**

    Toggle captions on or off.
*   **Color**

    Sets the text color.
*   **Font**

    Select a font style (such as heading or body) from your project’s theme.
*   **Size**

    Define the text size.
{% endcolumn %}

{% column %}
<figure><img src="../.gitbook/assets/CleanShot 2025-10-16 at 11 .52.29@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



{% columns %}
{% column %}
#### Lightbox

The Lightbox section controls how images are displayed when clicked. Enabling the Lightbox allows visitors to view larger versions of your images in a clean, focused overlay without leaving the page.

**Preview**

Toggle the Preview option to enable or disable viewing the lightbox in the Elements Editor.

**Media**\
Fine-tune the appearance of images displayed inside the lightbox.

*   **Radius**

    Adjust the corner rounding of lightbox images. Use Default to follow your project’s theme styling.
*   **Shadow**

    Apply a drop shadow around images in the lightbox to give them depth and contrast. Use Default to follow your project’s theme styling.

{% hint style="success" %}
**Tip:** Use consistent radius and shadow settings between your Thumbnails and Lightbox sections for a unified visual style.
{% endhint %}
{% endcolumn %}

{% column %}
<figure><img src="../.gitbook/assets/CleanShot 2025-10-16 at 12 .01.49@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



{% columns %}
{% column %}
#### Overlay

The Overlay section controls the background appearance behind images when the Lightbox is active. These settings let you adjust the overlay’s color, opacity, and blur to achieve the desired visual focus when viewing enlarged images.

**Color**

Choose the background color of the overlay.

* This determines the tone of the area behind the image when opened in the Lightbox.&#x20;
* Darker overlays help the image stand out, while lighter tones can create a softer presentation.

**Opacity**

Adjust the transparency of the overlay.

* Lower values make the background more visible through the overlay.
*   Higher values create a stronger contrast between the image and background.

    The default setting provides a subtle darkening effect suitable for most themes.

**Blur**

Adds a soft blur to the background content beneath the overlay.

* This helps draw attention to the image while maintaining a sense of depth and polish.&#x20;
* Increase the blur amount for a more diffused background effect.

{% hint style="success" %}
**Tip:** Combine a slightly dark overlay color with moderate blur for a clean, modern Lightbox appearance that complements most gallery styles.
{% endhint %}
{% endcolumn %}

{% column %}
<figure><img src="../.gitbook/assets/CleanShot 2025-10-16 at 12 .05.07@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}
