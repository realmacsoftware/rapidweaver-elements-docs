---
description: Compare two images or sets of content with an interactive slider
---

# Before After (Paid)

{% hint style="success" %}
Before After is available as a **paid product via the Elements Store**. Install the current version of Elements before adding it to a project.
{% endhint %}

Before After creates an interactive comparison that visitors can drag to reveal more or less of two images or two sets of components. It is ideal for photo edits, renovations, product comparisons, design revisions, and any situation where the difference is easier to understand visually.

The comparison can run horizontally or vertically, use a fixed or responsive height, and animate on hover or automatically. Content mode also lets you compare complete layouts rather than images alone.

<a href="elementsapp://storeProduct/com.elementsplatform.beforeafterpack" class="button primary" data-icon="store">Purchase Before After</a>

{% embed url="https://youtu.be/J0eU66LRuro" %}

### Features

* **Image and content modes** — Compare two images or place any Elements components on either side.
* **Flexible sizing** — Use an aspect ratio, a fixed height, or let the content determine the height.
* **Horizontal and vertical reveals** — Match the movement to the subject being compared.
* **Optional animation** — Animate on hover or move the divider automatically.
* **Custom divider and handle** — Set the starting position, thickness, colour, and handle visibility.
* **Touch-friendly interaction** — Visitors can drag the comparison on desktop and touch devices.

### Requirements

Before using Before After, make sure you have:

* The Before After pack installed from the Elements Store.
* Two suitable images, or two sets of child components when using Content mode.

{% hint style="warning" %}
Both sides should describe the same subject from a closely matched viewpoint. Large differences in dimensions or composition can make the comparison difficult to understand.
{% endhint %}

### Supported Content and File Types

Before After supports:

* Two image resources supported by Elements.
* Any Elements components placed in the Before and After dropzones.
* Responsive image and component-based comparisons.

### How to Use Before After

You’ll find Before After under **Media** in the Components list.

1. Drag **Before After** onto the page.
2. Choose **Images** or **Content** from the Mode setting.
3. Add the Before and After images, or place components into the two content dropzones.
4. Choose a Height Mode and Orientation.
5. Set the divider’s starting position and decide whether to show the handle.
6. Preview the page and test the comparison with a pointer and on a touch device.

### Component Settings

#### Before After

**Height Mode**

Controls how the component calculates its height.

* **Aspect Ratio** — Keeps the component at the selected proportion as its width changes. The default ratio is `7/5`.
* **Fixed Height** — Uses a height in pixels. The default is `500px`.
* **Dynamic (Content)** — Lets the child content determine the final height. The Initial Height setting provides a `500px` starting height while the content is being measured.

**Orientation**

* **Horizontal** — The divider moves from left to right.
* **Vertical** — The divider moves from top to bottom.

**Animate**

* **Off** — The divider only moves when a visitor drags it.
* **Hover** — The reveal follows the visitor’s hover position.
* **Auto** — The divider animates automatically.

When Hover or Auto is selected, **Duration** controls the animation time in seconds. The default is 3 seconds.

**Divider**

* **Start Position** — Sets the initial reveal point. The default is 50%.
* **Width / Height** — Controls divider thickness. Width appears for horizontal comparisons and Height appears for vertical comparisons.
* **Color** — Sets the divider colour.
* **Handle** — Shows or hides the draggable handle.

**Mode**

* **Images** — Displays the selected Before and After image resources.
* **Content** — Provides separate dropzones for complete component layouts.

In Content mode, **View In Edit** switches between the Before and After sides while you work in the editor.

{% columns %}
{% column width="50%" %}
#### Advanced

Use **Classes** to add custom CSS classes and **ID** to assign a unique HTML identifier.
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../../.gitbook/assets/CleanShot 2025-11-20 at 3 .13.53@2x.png" alt="Before After component Inspector with sizing, orientation, animation, divider, and content controls"><figcaption><p>The Before After settings in the Inspector.</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

### Accessibility

* Give both images useful descriptions in Resources. Describe the meaningful difference rather than repeating “before” and “after”.
* Keep the divider and handle visible with sufficient contrast so the interaction is easy to discover.
* Do not use the comparison as the only way to communicate essential information; include a short text explanation nearby.
* Avoid automatic movement when it is not necessary, and test the finished page with touch and pointer input.

### Tips and Best Practices

* **Match the source images:** Use the same crop, dimensions, and camera position for the clearest comparison.
* **Start near the centre:** A 50% starting position shows that both sides are available.
* **Use Content mode deliberately:** Keep the two layouts similar in size, especially when using Dynamic height.
* **Optimise images:** Resize and compress large originals before publishing.

### Troubleshooting

#### The component jumps or changes height

Use Aspect Ratio or Fixed Height when the two sides have different dimensions. In Content mode, also make sure both layouts have predictable heights.

#### The divider is difficult to see

Choose a divider colour that contrasts with both sides, increase its width or height, and enable the handle.

#### Only one content side is visible in the editor

Use **View In Edit** to switch between Before and After. Both sides appear in the published comparison.

### Related Components

* [Image Slider](../components/image-slider.md) — Present several images as a sequence rather than comparing two layers.
* [Image](../components/image.md) — Add and optimise individual image resources.

{% include "../../.gitbook/includes/common-controls.md" %}
