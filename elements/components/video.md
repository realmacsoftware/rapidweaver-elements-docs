---
description: Add YouTube, Vimeo, or MP4 video to a page
---

# Video

The Video component displays one YouTube, Vimeo, or MP4 video. It supports autoplay rules, start time, looping, player controls, a custom thumbnail, responsive framing, and an optional lightbox.

{% embed url="https://youtu.be/avzBCXIJFU0" %}

### Supported Content and File Types

* YouTube
* Vimeo
* MP4

Add a YouTube or Vimeo URL to Resources by dragging it from your browser. Add a local MP4 from Finder or import a remote URL.

{% hint style="success" %}
To use a video as a section background, choose Video in a [Container](container.md) background. [Watch the background video tutorial](https://youtu.be/x59UfuZvMwM).
{% endhint %}

### How to Use Video

You’ll find Video under **Media** in the Components list.

1. Add the video to Resources.
2. Drag **Video** onto the page.
3. Select the video under **Video → Resource**.
4. Choose autoplay, sound, controls, looping, and start time.
5. Configure the thumbnail, aspect ratio, and optional lightbox.
6. Preview playback in a browser.

The Video component also has a drop zone for a custom play button, text, or graphic.

### Component Settings

#### Video

**Autoplay**

* **Immediately** — Attempts to play when the page loads.
* **When in Viewport** — Plays when the video enters the viewport.
* **Never** — Waits for the visitor. This is the default.

**Muted** is enabled by default. Most browsers require muted audio for autoplay.

**Controls** shows or hides native player controls. **Loop** restarts the video when it finishes. These controls apply where supported by the selected video type.

**Time (seconds)** sets the playback start point and defaults to 0.

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-17 at 10 .40.54 2@2x.png" alt="Video Inspector controls for resource, autoplay, sound, controls, loop, and start time"><figcaption><p>The Video group controls the source and playback behaviour.</p></figcaption></figure>

#### Lightbox

**Enable** opens the video in an overlay and is off by default.

When enabled, **Color** defaults to Black, **Opacity** to 50%, and **Blur** to 0 pixels.

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-17 at 10 .45.09@2x.png" alt="Video Lightbox controls for backdrop colour, opacity, and blur"><figcaption><p>Lightbox backdrop controls.</p></figcaption></figure>

#### Thumbnail

**Type** can be Resource, Custom, or CMS. Resource is the default.

**Mode** switches between Light and Dark thumbnail sources. Custom uses a URL or path; CMS uses a field expression defaulting to `{{item.image.src}}`.

Custom and CMS thumbnails provide **Alt** text.

**Overlay Color** defaults to Surface 50 and **Opacity** to 50%.

{% hint style="info" %}
YouTube resources automatically provide a default thumbnail. Add your own when you need consistent branding or a different crop.
{% endhint %}

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-17 at 10 .48.49@2x.png" alt="Video Thumbnail controls for source, mode, image, alt text, and overlay"><figcaption><p>Thumbnail settings control the image shown before playback.</p></figcaption></figure>

#### Aspect Ratio

**Aspect Ratio** offers Auto, Wide 16:9, Tall 4:5, or Custom. Auto is the default; Custom defaults to `7/5`.

For a fixed ratio, **Object Fit** offers Fill, Contain, Cover, None, or Scale Down and defaults to Cover. **Position** sets the thumbnail focal point and defaults to Centre.

The aspect ratio controls the thumbnail frame rather than changing the source video’s dimensions.

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-01 at 4 .20.38@2x.png" alt="Video thumbnail Aspect Ratio controls with object fit and position options"><figcaption><p>Aspect Ratio controls the thumbnail frame and crop.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-01 at 4 .19.01@2x.png" alt="Video thumbnail Inspector showing custom aspect-ratio settings"><figcaption><p>A custom thumbnail ratio can use any valid x/y value.</p></figcaption></figure>

### Accessibility

Provide captions or a transcript for spoken content. Avoid unexpected audio, retain usable player controls, and describe custom thumbnails when they convey information.

### Tips and Best Practices

* **Mute autoplay:** It is required by most browsers and avoids surprising visitors.
* **Use an intentional thumbnail:** A compressed JPG usually offers good quality and performance.
* **Avoid autoplay for essential content:** Give visitors direct control over important videos.

### Related Components

* [Image](image.md) — Shares thumbnail source and aspect-ratio controls.
* [Gallery](gallery.md) — Combines several videos and images in one lightbox.
* [Container](container.md) — Supports background video.

{% include "../../.gitbook/includes/common-controls.md" %}
