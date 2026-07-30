---
description: Apply colour, image, gradient, SVG, video, and hover backgrounds
---

# Backgrounds

Background controls draw colour, images, gradients, SVGs, or video behind a component. The exact Style options depend on the selected component.

### Type and State

The general shared Background control defaults to:

* **Type** — None.
* **Style** — Color.
* **State** — Start.

**Type** is not responsive:

* **None** — Applies no background.
* **Static** — Uses one background.
* **Hover** — Provides separate Start and End backgrounds.

State appears for Hover and is not responsive. Add a [Transition](transitions.md) to animate compatible values.

### Color

**Color** selects a Theme Studio colour and **Opacity** ranges from 0–100%, defaulting to 100%.

Most common backgrounds default to Surface 50. The dedicated Background and Divider components use Brand 500.

### Gradient

**Type** defaults to Linear:

* **Linear** — Uses a Direction and defaults to To Bottom.
* **Radial** — Uses a Position and defaults to Centre.
* **Conic** — Uses an Angle and defaults to Default.

**Interpolation** defaults to Default. Other options include sRGB, HSL, OKLab, OKLCH, and hue-direction modes.

The default stops are:

| Stop | Colour | Opacity | Position |
| --- | --- | --- | --- |
| From | Brand 200 | 100% | 0% |
| Via | Brand 400 | 100% | 50% |
| To | Brand 500 | 100% | 100% |

**Add Via** is off by default. Enable it to reveal the middle stop.

### Image

Choose an image from Resources where the control provides an Image field. The dedicated Background component can also use a CMS field, which defaults to `{{item.image.src}}`.

Image defaults:

* **Position** — Centre.
* **Size** — Cover.
* **Repeat** — No Repeat.
* **Fetch Priority** — Auto.

Size options are Auto, Cover, and Contain. Repeat options are No Repeat, Repeat, Repeat Horizontal, and Repeat Vertical.

{% hint style="info" %}
Use High fetch priority only for a critical image visible when the page opens. Setting every background to High competes for bandwidth and can slow the page.
{% endhint %}

### SVG

The dedicated [Background component](../background.md) can use an SVG resource.

SVG defaults include:

* **Color** — Surface 500 at 100% opacity.
* **Fixed Width** and **Max Width** — 100%.
* **Min Width**, Fixed Height, Max Height, and Min Height — Auto.
* **Position** — Top 0, Right Auto, Bottom Auto, Left 0.
* **Translate X and Y** — 0.

The SVG’s own fill and stroke structure determines how the selected colour is applied.

### Video

Container backgrounds can use a video resource. **Aspect Ratio** is enabled by default and forces a 16:9 frame.

Use compressed, muted video and provide sufficient contrast between the video and foreground content.

### Background Overlay

Container provides a separate Background Overlay above its main background and behind its content. Use it to add tint, contrast, gradients, or effects without modifying the underlying image or video.

### Fixed Background

The dedicated Background component has a non-responsive **Fixed → Enabled** switch, which is off by default. Fixed backgrounds stay attached while the page scrolls.

Mobile browsers may limit or alter fixed-background behaviour for performance.

### Accessibility and Performance

* Keep text contrast readable across the complete image, gradient, or video.
* Do not communicate essential information through a decorative background alone.
* Optimise image and video resources before publishing.
* Check Hover backgrounds with keyboard focus and touch input; hover should enhance rather than reveal essential content.
