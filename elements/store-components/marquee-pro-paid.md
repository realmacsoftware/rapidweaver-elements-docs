---
description: Create a continuously scrolling strip of images or custom content
---

# Marquee Pro (Paid)

{% hint style="success" %}
Marquee Pro is available as a **paid product via the Elements Store**. Install the current version of Elements before adding it to a project.
{% endhint %}

Marquee Pro creates a continuously scrolling strip for logos, announcements, featured content, social links, promotions, and image collections. It can move horizontally or vertically and gives you control over speed, direction, spacing, edge fades, and visitor interaction.

Use a Resources folder for a quick image marquee, or use Items mode to build each repeated item from any Elements components.

<a href="elementsapp://storeProduct/com.elementsplatform.marqueepack" class="button primary" data-icon="store">Purchase Marquee Pro</a>

{% embed url="https://youtu.be/jbDbl_fV9Fo" %}

### Features

* **Folder and Items modes** — Scroll a folder of images or custom component-based items.
* **Horizontal and vertical layouts** — Match the marquee to the available space.
* **Responsive visible item count** — Control how much content is shown at each breakpoint.
* **Adjustable animation** — Set direction and duration from 1 to 300 seconds.
* **Hover and drag interactions** — Pause, slow, or let visitors drag through the content.
* **Gradient edge fade** — Soften the points where content enters and leaves.
* **Reduced-motion support** — Automatic movement stops when the visitor requests reduced motion.

### Requirements

Before using Marquee Pro, make sure you have:

* The Marquee Pro pack installed from the Elements Store.
* A Resources folder of images or at least one completed custom item.

{% hint style="warning" %}
Moving content should not be the only place important information appears. Visitors who request reduced motion will see a stationary marquee and need to be able to understand and use it in that state.
{% endhint %}

### Supported Content and File Types

Marquee Pro supports:

* Image resources from an Elements Resources folder.
* Any Elements components placed inside custom Items.
* Horizontal and vertical scrolling layouts.

### How to Use Marquee Pro

You’ll find Marquee Pro under **Interactive** in the Components list.

1. Drag **Marquee Pro** onto the page.
2. Choose Folder or Items from **Mode**.
3. Select an Image Folder, or add and populate the custom Items.
4. Set the visible Amount, layout Direction, and Gap.
5. Choose the animation Direction and Duration.
6. Preview the page at several widths and with reduced motion enabled.

### Component Settings

#### Content

**Mode**

* **Folder** — Displays every image in the selected Image Folder.
* **Items** — Creates a collection of custom items. Each item has a Title for editor organisation and a dropzone that accepts any components.

**Amount**

Sets the responsive number of visible items from 1 to 20. The default is 3.

**Direction**

Choose a **Horizontal** or **Vertical** layout.

**Gap**

Sets the responsive spacing between items using the theme spacing scale.

**Gradient Fade**

Enable a soft fade at the marquee edges. **Fade Size** controls its depth in pixels and defaults to 100px.

#### Animation

**Direction**

Sets the flow to the left or right. In a vertical layout, the same setting determines the corresponding vertical flow.

**Duration**

Sets how long a complete animation cycle takes, from 1 to 300 seconds. The default is 20 seconds. A larger value produces slower movement.

**On Hover**

* **Pause** — Stops automatic movement while the pointer is over the marquee.
* **Slow** — Changes to the Hover Duration while hovered. The default is 60 seconds, with a range of 1 to 600 seconds.
* **None** — Keeps the normal animation speed.

**Draggable Scroll**

Lets visitors drag or swipe the track manually. It is off by default.

#### Size

**Height**

Sets a responsive theme or custom height. The default is Auto. Give vertical marquees a defined height so there is a clear viewport for the movement.

**Width**

Sets the responsive component width. The default is 100%.

#### Advanced

Use **Classes** to add custom CSS classes and **ID** to assign a unique HTML identifier.

### Accessibility

* Marquee Pro watches the visitor’s `prefers-reduced-motion` setting and stops automatic animation when Reduce Motion is enabled.
* Enable Draggable Scroll when visitors may need to reach content that sits outside the stationary viewport.
* Use Pause for moving items that contain links or controls so they remain easier to target.
* Add useful alternative text to folder images and keep essential information elsewhere on the page as well.

### Tips and Best Practices

* **Move slowly:** Start with the 20-second default and increase it for long strips or detailed content.
* **Size by content:** Three visible items is a good starting point; logos can often be smaller, while cards need more space.
* **Use similar item dimensions:** Consistent shapes create a smoother loop.
* **Optimise folder images:** Resize and compress them before publishing.
* **Use a vertical height:** Auto works for horizontal strips, but vertical marquees need a predictable viewport.

### Troubleshooting

#### The marquee is not moving

Check the visitor’s Reduce Motion preference first. Also confirm the Duration is valid and that the marquee contains enough items to form a scrolling track.

#### A vertical marquee has no useful height

Set a responsive Height in the Size group rather than leaving it on Auto.

#### Folder images are missing

Confirm that Mode is Folder, Image Folder points to a folder resource, and the folder contains supported images.

#### Custom content cannot be found

Switch Mode to Items, add an item to the collection, and place components in that item’s dropzone.

### Related Components

* [Content Slider](../components/content-slider.md) — Use a user-controlled sequence instead of continuous movement.
* [Gallery](../components/gallery.md) — Present a static, structured collection of images.

{% include "../../.gitbook/includes/common-controls.md" %}
