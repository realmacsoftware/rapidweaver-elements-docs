---
description: Build a responsive masonry layout from a folder of images
---

# Masonry Images (Free)

{% hint style="success" %}
Masonry Images is available as a **free download via the Elements Store**. Install the current version of Elements before adding it to a project.
{% endhint %}

Masonry Images turns a Resources folder into a responsive, multi-column image layout. Images keep their natural proportions and flow into columns of different heights, making the component well suited to portfolios, mood boards, event photos, and editorial image collections.

Because the component reads directly from a folder, adding, removing, or reordering resources is a quick way to maintain the published layout.

<a href="elementsapp://storeProduct/com.elementsplatform.masonryimagespack" class="button primary" data-icon="store">Get Masonry Images</a>

{% embed url="https://www.youtube.com/watch?v=dTeDSg-cfzM" %}

### Features

* **Folder-based setup** — Build and maintain the layout from one Resources folder.
* **Two masonry engines** — Choose a CSS column layout or a JavaScript-balanced layout.
* **Responsive columns** — Set different column counts at each breakpoint.
* **Theme spacing** — Control the gap with the project’s spacing scale.
* **Image styling** — Apply radius, shadow, hover, and responsive resize settings.

### Requirements

Before using Masonry Images, make sure you have:

* The Masonry Images pack installed from the Elements Store.
* A Resources folder containing image resources.

{% hint style="warning" %}
CSS Masonry and JS Masonry can arrange the same images differently. Always check the published result in an external browser, especially after changing image order or responsive columns.
{% endhint %}

### Supported Content and File Types

Masonry Images supports:

* Image resources supported by Elements.
* A single Resources folder as the image source.
* Responsive resized image output.

### How to Use Masonry Images

You’ll find Masonry Images under **Media** in the Components list.

1. Add or select a folder in Resources and place your images inside it.
2. Drag **Masonry Images** onto the page.
3. Choose the folder from **Resources** in the Inspector.
4. Select CSS Masonry or JS Masonry.
5. Set the responsive Columns, Gap, and image styling.
6. Preview the page in an external browser at several widths.

### Component Settings

#### Media

**Resources**

Selects the Resources folder used to build the layout. Add or remove images from this folder to update the component.

#### Layout

**Mode**

* **CSS Masonry** — Uses CSS columns. It is lightweight and follows column flow, so items usually fill down one column before moving to the next.
* **JS Masonry** — Uses JavaScript in the browser to balance images across columns.

**Columns**

Sets the number of columns at each responsive breakpoint, from 1 to 8. Use fewer columns on small screens so thumbnails remain large enough to understand.

**Gap**

Sets the spacing between images using the theme spacing scale.

#### Images

**Border Radius**

Controls the corner rounding for every image.

**Shadow**

Applies a theme shadow to the images.

**Hover Effect**

* **None** — Leaves the image unchanged.
* **Zoom** — Enlarges the image within its frame. **Zoom Level** ranges from 100% to 200% and defaults to 110%.
* **Lift** — Moves the image slightly upward and adds depth.

**Width**

Controls the generated image width at each breakpoint. The defaults are 400px at Base, 600px at SM, 800px at MD, and 1200px at LG.

#### Advanced

Use **Classes** to add custom CSS classes and **ID** to assign a unique HTML identifier.

### Accessibility

* Add an accurate description to each image resource. Masonry Images uses the resource description as alternative text.
* Keep the layout order meaningful because CSS and JS modes can present images in different visual columns.
* Do not communicate essential information only through a hover effect.
* Check that images remain large enough and sufficiently clear at every breakpoint.

### Tips and Best Practices

* **Prepare images first:** Resize and compress large source files before adding them to Resources.
* **Use consistent subject matter:** A varied set of proportions works well, but a coherent collection feels more intentional.
* **Choose columns by content:** Portrait images can support more columns than detailed screenshots or images containing text.
* **Compare both modes:** JS Masonry often gives a more balanced lower edge; CSS Masonry provides predictable column flow.

### Troubleshooting

#### No images appear

Confirm that Resources points to a folder rather than an individual file and that the folder contains supported image resources.

#### The image order looks unexpected

CSS Masonry follows column flow, while JS Masonry balances items by available space. Try the other Mode and verify the order in an external browser.

#### Images look soft

Increase the responsive Width values so the generated images are large enough for their displayed size.

### Related Components

* [Gallery](../components/gallery.md) — Use the included gallery when you want a conventional image grid.
* [Gallery Pro](gallery-pro.md) — Add lightbox, video, albums, metadata, and more advanced gallery controls.

{% include "../../.gitbook/includes/common-controls.md" %}
