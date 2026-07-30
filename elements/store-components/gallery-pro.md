---
description: Build responsive image and video galleries with albums, metadata, and a lightbox
---

# Gallery Pro (Paid)

{% hint style="success" %}
Gallery Pro is available as a **paid product via the Elements Store** and requires **Elements 2.0 or newer**.
{% endhint %}

Gallery Pro is a flexible gallery for photographers, designers, and creators who need more than a basic image grid. It combines responsive Grid and Masonry layouts with image and video support, automatic albums, detailed metadata, and a configurable full-screen lightbox.

Use it for a focused portfolio, a large collection organised into subfolders, or a mixed-media gallery containing photographs, YouTube and Vimeo links, and MP4 video.

<a href="elementsapp://storeProduct/com.elementsplatform.gallerypropack" class="button primary" data-icon="store">Purchase Gallery Pro</a>

{% embed url="https://youtu.be/qO-t9FZ5IQo" %}

### Features

* **Grid and two Masonry layouts** — Choose uniform crops, CSS columns, or a JavaScript-balanced arrangement.
* **Images and video** — Combine JPG, PNG, MP4, YouTube, and Vimeo resources.
* **Automatic albums** — Turn Resources subfolders into browsable sub-galleries.
* **Thumbnail metadata** — Display captions, authors, and selected EXIF fields below or over images.
* **Configurable lightbox** — Control transitions, navigation, zoom, fullscreen, autoplay, thumbnails, and media sizing.
* **Lightbox metadata** — Show a separate caption, author, and EXIF presentation in the expanded view.
* **Video playback options** — Set autoplay, mute, loop, controls, preload, and mobile inline playback.
* **Responsive image sizing** — Generate appropriate thumbnail and lightbox image widths.
* **Casual image protection** — Discourage right-clicking and dragging when needed.

### Requirements

Before using Gallery Pro, make sure you have:

* Elements 2.0 or newer.
* The Gallery Pro pack installed from the Elements Store.
* A Resources folder containing supported images, videos, or video links.
* Captions, authors, alternative text, and EXIF data added to the relevant resources when those fields should appear.

{% hint style="warning" %}
Image Protection can discourage casual downloading, but it cannot prevent a determined visitor from retrieving files delivered to their browser. Do not use it as a substitute for suitable publishing permissions, watermarking, or appropriately sized source images.
{% endhint %}

### Supported Content and File Types

Gallery Pro supports:

* JPG and PNG image resources.
* MP4 video resources.
* YouTube and Vimeo links added to Resources.
* Subfolders used as automatic albums.

{% hint style="success" %}
To add YouTube or Vimeo media, drag the video or playlist URL from a browser into the Resources area in Elements.
{% endhint %}

### How to Use Gallery Pro

You’ll find Gallery Pro under **Media** in the Components list.

1. Create a folder in Resources and add the images, videos, and video links for the gallery.
2. Add captions, author details, descriptions, and EXIF metadata to the resources where needed.
3. Drag **Gallery Pro** onto the page and choose the folder under **Resources**.
4. Select Grid, CSS Masonry, or JS Masonry and set responsive Columns and Gap.
5. Configure thumbnail appearance and metadata.
6. Enable and style the lightbox, then choose its controls, transitions, media size, and metadata.
7. Preview the lightbox in an external browser at desktop and mobile widths.

### Organise Galleries and Albums

Gallery Pro reads the contents of the selected Resources folder. If that folder contains subfolders, each subfolder becomes an album and its first image is used as the album cover. Selecting the cover opens the album’s contents in the lightbox.

Keep related media together, put the preferred cover first, and avoid deeply nested or inconsistently named folders.

### Prepare Images for Publishing

For a sharp result on modern displays, use source images that are at least as wide as the largest lightbox size you intend to serve. The default Lightbox Max Width is 1200px, while the responsive thumbnail defaults rise to 1200px at the LG breakpoint.

Large originals increase upload size and page weight. Resize and compress them before publishing; [Squash for macOS](https://www.realmacsoftware.com/squash/) can process a folder in one batch.

### Component Settings

#### Media

**Resources**

Selects the folder used to build the gallery and its albums.

**Image Protection**

When enabled, Gallery Pro disables casual right-clicking and dragging and places protective overlays over images. The files still reach the browser and remain accessible to determined visitors.

#### Layout

**Mode**

* **Grid** — Displays uniform rows and enables the thumbnail Ratio setting.
* **CSS Masonry** — Uses CSS columns and preserves natural image proportions.
* **JS Masonry** — Uses JavaScript in the browser to balance items across columns.

**Columns**

Sets a responsive column count from 1 to 8. The default is 3.

**Gap**

Sets responsive spacing between gallery items using the theme spacing scale.

{% hint style="info" %}
CSS Masonry and JS Masonry can produce different image orders and lower edges. Check Masonry layouts in an external browser rather than relying only on the editor.
{% endhint %}

#### Thumbnails

**Ratio**

Available in Grid mode:

* **Square** — Crops thumbnails to `1/1`. This is the default.
* **Wide** — Uses a `7/5` landscape crop.
* **Tall** — Uses a `4/5` portrait crop.
* **Auto** — Preserves the source proportions.

**Radius and Shadow**

Apply theme border-radius and shadow values to every thumbnail.

**Width**

Controls generated thumbnail width at each responsive breakpoint. The defaults are 400px at Base, 600px at SM, 800px at MD, and 1200px at LG.

**Hover Effect**

* **None** — No thumbnail movement.
* **Zoom** — Enlarges the image within its frame. Zoom Level ranges from 100% to 200% and defaults to 110%.
* **Lift** — Raises the thumbnail and adds visual depth.

#### Thumbnails Meta Data

**Type**

* **Hidden** — Hides thumbnail metadata. This is the default.
* **Below** — Places metadata after the image. Below is not supported by Masonry layouts.
* **Overlay** — Places metadata over the image.

**Margin and Alignment**

Below metadata has a theme spacing margin. Text can align Left, Center, or Right; Center is the default.

**Overlay**

Choose **Always**, **Slide In**, or **Fade In**, then set the background colour, opacity, and padding. Overlay opacity defaults to 80%.

**Caption and Author**

Each field can be shown independently and styled with colour, font, size, and weight. Author also has a separate margin. Both are enabled by default when metadata itself is displayed.

**EXIF**

Enable EXIF, then choose:

* Horizontal or Vertical direction.
* Left, Center, or Right alignment.
* Margin, gap, optional icons, colour, font, size, and weight.
* Aperture, Shutter, ISO, Focal Length, Lens, and Date fields.

Aperture, Shutter, ISO, and Focal Length are enabled by default. Lens and Date are off by default.

#### Lightbox

The Lightbox group controls behaviour. Preview it in an external browser.

**Enabled**

Turns the lightbox on or off at responsive breakpoints.

**Deep Linking**

Updates the URL hash while an item is open so a specific gallery item can be linked directly. It is off by default.

**Overlay**

Sets the expanded view’s background colour and opacity.

**Animated Thumbnails**

Animates from the selected thumbnail into the lightbox. It is enabled by default with a 400ms duration.

**Transition**

Choose Slide, Fade, Zoom In, Zoom In (Large), Zoom Out, Zoom Out (Large), Soft Zoom, Scale Up, Slide Circular, Rotate, or Tube. Set Speed in milliseconds and choose Ease, Linear, Ease In, Ease Out, or Ease In Out. The defaults are Slide, 400ms, and Ease.

**Controls and Behaviour**

Enable or disable:

* Counter — enabled by default.
* Zoom — enabled by default.
* Download — disabled by default and downloads the original image when enabled.
* Rotate and flip controls — disabled by default.
* Close button — enabled by default.
* Previous and Next controls — enabled by default.
* Loop — enabled by default.
* Close on Tap — enabled by default.
* Swipe to Close — enabled by default.
* Mousewheel navigation — disabled by default.
* Hide Scrollbar — disabled by default.
* Fullscreen — enabled by default.

**Autoplay**

Automatic advancement is off by default. When enabled, set the Interval in milliseconds; the default is 5000ms. The progress bar is enabled by default.

#### Lightbox Style

Set the navigation arrow colour, background, and opacity; toolbar icon colour; counter colour; and autoplay progress bar colour. Arrow background opacity defaults to 45%.

#### Lightbox Thumbnails

Enable the navigation strip, then set:

* Aspect Ratio — Square, 5:4, 4:3, or 16:9. The default is 5:4.
* Size — 100px by default.
* Spacing — 5px by default.
* Border radius, size, normal colour, and active colour.
* Background colour.

#### Lightbox Media

**Max Width**

Choose 1200px, 1600px, 2400px, or Original. The default is 1200px. Larger values increase transfer size; Original bypasses lightbox resizing.

**Radius and Shadow**

Apply theme radius and shadow values to expanded media.

#### Lightbox Meta Data

**Type**

Choose Hidden or Below. Below is the default.

**Margin and Alignment**

Set the spacing below the media and align the metadata Left, Center, or Right.

**Caption, Author, and EXIF**

These provide the same styling and field controls as thumbnail metadata, but are configured independently for the lightbox. Caption, Author, and EXIF display are off by default. Aperture, Shutter, ISO, and Focal Length are preselected when EXIF is enabled; Lens and Date are off.

#### Videos

**Playback**

* **Autoplay** — Starts video when opened. It is off by default, and most browsers require Muted for autoplay.
* **Muted** — Starts without sound. It is off by default.
* **Loop** — Repeats playback. It is off by default.

**Show Controls**

Displays the browser’s playback controls and is enabled by default.

**Preload**

* **None** — Avoids loading video data in advance.
* **Metadata** — Loads duration and dimensions. This is the default.
* **Auto** — Lets the browser decide what to preload.

**Plays Inline**

Keeps video within the page on supported mobile browsers rather than forcing fullscreen. It is enabled by default.

**Thumbnail Overlay and Play Button**

Set overlay colour and opacity, plus play button background, opacity, and icon colour. Default opacities are 20% for the overlay and 50% for the button.

#### Advanced

Use **Classes** to add custom CSS classes and **ID** to assign a unique HTML identifier.

### Accessibility

* Add a meaningful description to every image resource; captions and filenames are not a substitute for useful alternative text.
* Keep Close, Previous/Next, and video controls available unless there is another obvious, keyboard-accessible way to perform the same actions.
* Provide captions or transcripts for video content and avoid autoplay with sound.
* Ensure metadata overlays have sufficient text and background contrast in their normal and hover states.
* Do not rely on hover-only metadata for essential information; touch and keyboard users may not receive the same hover state.
* Check focus movement when opening and closing the lightbox in the published gallery.

### Tips and Best Practices

* **Use Grid for consistency:** It is the best choice when uniform thumbnail crops matter.
* **Compare Masonry modes:** CSS gives column flow; JS generally produces a more balanced lower edge.
* **Keep image sizes intentional:** Match generated widths to their maximum displayed size rather than always serving Original.
* **Put album covers first:** The first image in a subfolder represents that album.
* **Use metadata selectively:** A few useful fields are easier to scan than every available EXIF value.
* **Protect performance:** Compress images, use video Preload Metadata or None, and avoid an unnecessarily large lightbox Max Width.

### Troubleshooting

#### The Below metadata option does not appear correctly

Below thumbnail metadata is not supported in Masonry modes. Switch Layout Mode to Grid or use Overlay metadata.

#### The lightbox looks different from the editor

Open the page in an external browser. Lightbox behaviour, JS Masonry, fullscreen, video playback, and browser controls cannot be judged reliably from the editor alone.

#### Autoplay video does not start

Enable Muted as well as Autoplay. Browser autoplay policies normally block video that begins with sound.

#### EXIF values are missing

Confirm that the source file contains the selected EXIF fields and that the resource has not been processed in a way that strips metadata.

#### YouTube or Vimeo media is missing

Drag the video URL into Resources and confirm it belongs to the folder selected by Gallery Pro.

#### The gallery loads slowly

Reduce thumbnail Width and Lightbox Max Width, compress source images, avoid Original unless necessary, and set video Preload to Metadata or None.

### Related Components

* [Gallery](../components/gallery.md) — Use the included component for a simpler image gallery.
* [Masonry Images](masonry-images-free.md) — Create a lightweight folder-based masonry layout without a lightbox or metadata.
* [Video](../components/video.md) — Present a single video with direct playback controls.

{% include "../../.gitbook/includes/common-controls.md" %}
