---
description: A Powerful, Professional Gallery for Photographers and Creators
---

# Gallery Pro (Paid)

Gallery Pro is a powerful, professional-grade photo gallery component for Elements, built for photographers, designers, and creators who want their work to shine.

{% embed url="https://youtu.be/qO-t9FZ5IQo" %}

Effortlessly organise images into beautiful, responsive layouts, create sub-galleries for larger collections, and present your photos in an immersive slideshow experience. With support for EXIF data and flexible title, author, and caption displays, Gallery Pro keeps your images informative as well as stunning.

Gallery Pro gives you the control and polish needed to present your photography at its absolute best.

<a href="elementsapp://storeProduct/com.elementsplatform.gallerypropack" class="button primary" data-icon="store">Purchase Gallery Pro</a>

Gallery Pro is **available via the Elements Store** and requires **Elements 2.0 or newer**.

### Features

* Beautiful **Grid** and **Masonry** layout options for flexible, responsive galleries
* Support for **images and video** including YouTube, Vimeo, local, and remote sources
* **Automatic sub-galleries** to organise large collections with ease
* **EXIF data support** to display detailed photo information
* Flexible **title, author, and caption** display on thumbnails and in the slideshow
* Stylish **thumbnail hover effects** such as Zoom and Lift
* **10+ professional slideshow transitions** for polished presentations
* Immersive **full-screen lightbox** viewing with intuitive controls
* Interactive **pan and zoom** controls for detailed image viewing
* Built-in **rotate and flip** controls for perfect orientation
* And so much more…

#### Supported File Types

Gallery Pro supports the following media:

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
**Media**

Drop a folder of images, videos, YouTube links, or Vimeo links into the dropzone to build your gallery.

{% hint style="success" %}
You can **add YouTube or Vimeo videos** by dragging and dropping the URL from your web browser to the Resources area in RapidWeaver Elements. A playlist URL can also be dropped into the resources area.
{% endhint %}

{% hint style="info" %}
**Album Mode:** If your folder contains sub-folders, Gallery Pro will automatically create albums. Each sub-folder becomes its own album, with the first image used as the album cover. Clicking an album opens its contents in the lightbox.
{% endhint %}
{% endcolumn %}

{% column width="50%" %}

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
#### Layout

The Layout section controls how your images are arranged within the Gallery Pro component. Choose a layout mode, set the number of columns, and define the spacing between each thumbnail.

**Mode**

Select how images are laid out across the gallery.

*   **Grid**

    A uniform grid layout where all thumbnails share the same aspect ratio, giving a clean, structured appearance.
*   **CSS Masonry**

    A CSS-based masonry layout that preserves each image's natural aspect ratio. Images are arranged in columns with varying heights, creating a Pinterest-style layout.
*   **JS Masonry**

    A JavaScript-based balanced masonry layout that intelligently distributes images across columns to minimise uneven column heights. This produces a tighter, more balanced result than CSS Masonry.

{% hint style="success" %}
**Tip:** Use Grid mode for a polished, uniform look. Choose CSS Masonry or JS Masonry when you want to preserve each image's original proportions. JS Masonry generally produces a more balanced layout than CSS Masonry.
{% endhint %}

**Columns**

Adjust the number of columns displayed in your gallery.

* Use the slider to set between 1 and 8 columns of thumbnails across your layout.
* The gallery automatically adapts to different screen sizes, ensuring images remain evenly spaced and visually balanced.

**Gap**

Set the spacing between gallery items.

* The Gap value defines the amount of space between thumbnails.
* Use smaller values for a tighter grid or larger ones to give each image more breathing room.
* The value corresponds to the theme spacing scale, so it remains consistent with your theme settings.
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
**Thumbnails**

The Thumbnails section controls the appearance of image thumbnails within your gallery. You can adjust the aspect ratio, shape, shadow, and hover behaviour to suit your project's style.

{% hint style="warning" %}
The Aspect Ratio setting is only available in Grid mode. In Masonry modes, each image retains its natural proportions.
{% endhint %}

**Ratio**

Choose the aspect ratio for your thumbnails (Grid mode only).

*   **Square (1/1)**

    Crops all thumbnails to a square shape.
*   **Wide (7/5)**

    A landscape-oriented crop, great for scenic or panoramic images.
*   **Tall (4/5)**

    A portrait-oriented crop, ideal for headshots or vertical compositions.
*   **Auto**

    Preserves each image's original aspect ratio within the grid.

**Radius**

Adjust the corner rounding of your thumbnail images. Use Default to follow your project's theme styling, or set a custom value.

**Shadow**

Adds a soft drop shadow to thumbnails. Use Default to follow your project's theme styling, or choose a custom shadow level for more depth.

**Hover Effect**

Choose how thumbnails respond when a visitor hovers over them.

*   **None**

    No hover animation.
*   **Zoom**

    The image scales up slightly on hover, drawing attention to it. Use the **Zoom Level** slider (100–200%) to control how much the image enlarges.
*   **Lift**

    The thumbnail shifts upward slightly and gains a subtle shadow, creating a raised, interactive feel.
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
**Thumbnail Meta Data**

Control how metadata (captions, author names, and EXIF data) is displayed on your gallery thumbnails. You can show metadata below the image, as an overlay on top of it, or hide it entirely.

**Display Type**

Choose where metadata appears in relation to the thumbnail.

*   **Hidden**

    No metadata is shown on thumbnails.
*   **Below**

    Metadata appears directly beneath each thumbnail image.
*   **Overlay**

    Metadata is displayed on top of the thumbnail. When Overlay is selected, additional options become available to control the trigger animation and background styling.

**Alignment**

Align metadata text to the Left, Center, or Right of each thumbnail.

**Overlay Trigger**

When Display Type is set to Overlay, choose how the metadata overlay appears.

*   **Always**

    The overlay is always visible on the thumbnail.
*   **Slide In**

    The overlay slides up from the bottom on hover.
*   **Fade In**

    The overlay fades in on hover.

**Overlay Background**

Style the background behind the overlay text for improved readability.

*   **Color**

    Set the overlay background colour.
*   **Opacity**

    Control the transparency of the overlay background (0–100%).
*   **Padding**

    Adjust the inner spacing around the overlay text.

**Caption**

Controls the appearance of the image caption on thumbnails.

*   **Show**

    Toggle captions on or off.
*   **Color**

    Sets the text colour.
*   **Font**

    Select a font style from your project's theme.
*   **Size**

    Define the text size.
*   **Weight**

    Set the font weight (e.g. light, regular, bold).

**Author**

Controls the appearance of the author name on thumbnails. Offers the same settings as Caption: Show, Color, Font, Size, and Weight.

**EXIF**

Display photographic metadata (shooting information) on your thumbnails.

*   **Show**

    Toggle EXIF data display on or off.
*   **Direction**

    Display EXIF items in a Row (horizontal) or Column (vertical) layout.
*   **Alignment**

    Align EXIF data to the left, centre, or right.
*   **Gap**

    Set the spacing between individual EXIF items.
*   **Icons**

    Toggle EXIF icons on or off for a cleaner or more visual presentation.
*   **Color, Font, Size, Weight**

    Customise the typography of EXIF text.

**EXIF Properties**

Choose which EXIF fields to display. Each can be individually toggled on or off:

* Aperture
* Shutter Speed
* ISO
* Focal Length
* Lens
* Date

{% hint style="success" %}
**Tip:** EXIF data is read directly from your image files. Make sure your images retain their EXIF metadata for these fields to appear.
{% endhint %}
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
**Lightbox**

The Lightbox section controls the full-screen image viewing experience. When a visitor clicks a thumbnail, the lightbox opens with a range of controls, transitions, and behaviours that you can customise here.

**Overlay**

Style the background behind the lightbox.

*   **Color**

    Choose the background colour of the lightbox overlay. Darker colours help images stand out, while lighter tones create a softer presentation.
*   **Opacity**

    Adjust the transparency of the overlay (0–100%). Higher values create stronger contrast between the image and the page behind it.

**Animated Thumbnails**

When enabled, the lightbox thumbnail smoothly animates into the full-size view when opened.

*   **Enabled**

    Toggle the opening animation on or off.
*   **Duration**

    Set the animation speed in milliseconds (default: 400ms).

**Transition**

Control how images transition when navigating between them in the lightbox.

*   **Mode**

    Choose from over 10 transition effects, including Slide, Fade, Zoom In, Zoom Out, Rotate, Tube, and more.
*   **Speed**

    Set the transition duration in milliseconds (default: 400ms).
*   **Easing**

    Choose the acceleration curve for transitions: Ease, Linear, Ease In, Ease Out, or Ease In Out.

**Counter**

Toggle the image counter (e.g. "3 / 12") on or off in the lightbox toolbar.

**Zoom**

Enable or disable pinch-to-zoom and click-to-zoom functionality within the lightbox.

**Download**

When enabled, adds a download button to the lightbox toolbar allowing visitors to save images.

**Rotate**

When enabled, adds rotate and flip controls to the lightbox toolbar, letting visitors adjust image orientation.

**Close Button**

Toggle the close button visibility in the lightbox toolbar.

**Prev/Next Controls**

Show or hide the previous and next navigation arrows in the lightbox.

**Loop**

When enabled, navigating past the last image wraps back to the first image, and vice versa.

**Close on Tap**

When enabled, tapping on the overlay area (outside the image) closes the lightbox.

**Swipe to Close**

When enabled, visitors can swipe vertically to dismiss the lightbox on touch devices.

**Mousewheel**

When enabled, allows navigating between images using the mouse scroll wheel.

**Hide Scrollbar**

When enabled, hides the page scrollbar while the lightbox is open for a cleaner full-screen experience.

**Autoplay**

Automatically advance through images in a slideshow.

*   **Enabled**

    Toggle autoplay on or off.
*   **Interval**

    Set the time between slides in milliseconds (default: 5000ms).
*   **Progress Bar**

    When enabled, displays a progress bar showing the time remaining before the next slide.

**Fullscreen**

Enable or disable the fullscreen button in the lightbox toolbar. When activated, visitors can expand the lightbox to fill the entire screen.

{% hint style="success" %}
**Tip:** For a cinematic presentation, enable Autoplay with a 4–6 second interval, set the Transition to Fade, and enable Fullscreen. This creates a polished, hands-off slideshow experience.
{% endhint %}
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
**Lightbox Style**

The Lightbox Style section lets you customise the colours of the lightbox interface elements to match your project's theme.

**Navigation Arrows**

Style the previous/next navigation arrows displayed in the lightbox.

*   **Color**

    Set the colour of the arrow icons.
*   **Background**

    Set the background colour of the arrow buttons.
*   **Background Opacity**

    Adjust the transparency of the arrow button backgrounds (0–100%).

**Toolbar Icons**

*   **Color**

    Set the colour of the toolbar icons (close, zoom, download, rotate, fullscreen).

**Counter**

*   **Color**

    Set the colour of the image counter text.

**Progress Bar**

*   **Color**

    Set the colour of the autoplay progress bar.

{% hint style="success" %}
**Tip:** For best results, use semi-transparent arrow backgrounds with high-contrast icon colours. This keeps navigation controls visible without distracting from the images.
{% endhint %}
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
**Lightbox Thumbnails**

The Lightbox Thumbnails section controls the thumbnail strip displayed at the bottom of the lightbox. This strip provides quick navigation between images.

**Enabled**

Toggle the thumbnail strip on or off.

**Aspect Ratio**

Set the aspect ratio for thumbnails in the strip.

* Square (1/1), Landscape (5/4), Wide (4/3), or Widescreen (16/9).

**Size**

Set the size of each thumbnail in pixels (default: 100px).

**Spacing**

Set the gap between thumbnails in pixels (default: 5px).

**Border**

Style the border around lightbox thumbnails.

*   **Radius**

    Set the corner rounding of thumbnails (default: 4px).
*   **Size**

    Set the border width in pixels (default: 0px).
*   **Color**

    Set the border colour for inactive thumbnails.
*   **Active Color**

    Set the border colour for the currently active thumbnail, providing a clear visual indicator of the selected image.

**Background**

*   **Color**

    Set the background colour of the thumbnail strip area.
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
**Lightbox Media**

Fine-tune the appearance of images displayed inside the lightbox.

**Radius**

Adjust the corner rounding of lightbox images. Use Default to follow your project's theme styling.

**Shadow**

Apply a drop shadow around images in the lightbox to give them depth and contrast. Use Default to follow your project's theme styling.

{% hint style="success" %}
**Tip:** Use consistent radius and shadow settings between your Thumbnails and Lightbox Media sections for a unified visual style.
{% endhint %}
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
**Lightbox Meta Data**

Control how metadata is displayed within the lightbox when viewing full-size images. This section mirrors many of the Thumbnail Meta Data options, allowing you to show different levels of detail in the lightbox.

**Display Type**

Choose where metadata appears in the lightbox.

*   **Hidden**

    No metadata is shown in the lightbox.
*   **Below**

    Metadata appears directly beneath the full-size image.

**Margin**

Adds spacing between the image and the metadata area below it. The value corresponds to the theme spacing scale.

**Alignment**

Align metadata text to the Left, Center, or Right.

**Caption**

Controls the appearance of the image caption in the lightbox.

*   **Show**

    Toggle captions on or off.
*   **Color**

    Sets the text colour.
*   **Font**

    Select a font style from your project's theme.
*   **Size**

    Define the text size.
*   **Weight**

    Set the font weight.

**Author**

Controls the appearance of the author name in the lightbox. Offers the same settings as Caption: Show, Color, Font, Size, and Weight.

**EXIF**

Display photographic metadata within the lightbox.

*   **Show**

    Toggle EXIF data display on or off.
*   **Direction**

    Display EXIF items in a Row (horizontal) or Column (vertical) layout.
*   **Alignment**

    Align EXIF data to the left, centre, or right.
*   **Gap**

    Set the spacing between individual EXIF items.
*   **Icons**

    Toggle EXIF icons on or off.
*   **Color, Font, Size, Weight**

    Customise the typography of EXIF text.

**EXIF Properties**

Choose which EXIF fields to display in the lightbox. Each can be individually toggled:

* Aperture
* Shutter Speed
* ISO
* Focal Length
* Lens
* Date
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
**Videos**

The Videos section controls the playback behaviour of video content within your gallery. These settings apply to local .mp4 videos as well as YouTube and Vimeo embeds.

**Autoplay**

When enabled, videos begin playing automatically when opened in the lightbox.

**Muted**

When enabled, videos start with the audio muted. This is often required by browsers for autoplay to function.

{% hint style="warning" %}
Most browsers require videos to be muted for autoplay to work. If you enable Autoplay, consider also enabling Muted for reliable playback.
{% endhint %}

**Loop**

When enabled, videos restart automatically when they reach the end.

**Show Controls**

Toggle the video player controls (play/pause, volume, progress bar, fullscreen) on or off.

**Preload**

Control how much video data is loaded before the visitor presses play.

*   **None**

    No video data is preloaded. Best for bandwidth-conscious sites.
*   **Metadata**

    Only loads video metadata (duration, dimensions). This is the default and a good balance between performance and usability.
*   **Auto**

    The browser decides how much video data to preload. May load the full video.

**Plays Inline**

When enabled, videos play inline on mobile devices rather than entering the device's native fullscreen player. This provides a more seamless browsing experience on iOS devices.
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
**Advanced**

The [Advanced Section](../elements/components/common-controls/advanced.md) provides options for users who want finer control over styling or need to link directly to the Gallery Pro component.

These settings are ideal for developers and advanced users comfortable with custom CSS or Tailwind utilities.

**Deep Linking**

When enabled, each image in the gallery is assigned a unique URL hash. This allows visitors to share direct links to specific images, and the lightbox will open to the correct image when the link is visited.

{% hint style="success" %}
**Tip:** Deep Linking is especially useful for photographers who want to share direct links to individual images in their portfolio.
{% endhint %}

**CSS Classes**

Add one or more Tailwind CSS classes to the Gallery Pro component for custom styling.

This allows you to extend or override default styles without editing your theme or component code.

You can use any valid Tailwind utility class to adjust spacing, colours, borders, or animations.

**ID**

Assign a unique ID to the component. This is useful for creating in-page [anchor links](../elements/components/common-controls/advanced.md#id) or targeting the component with custom scripts and CSS selectors.
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}
