---
description: Display images in a swipeable, responsive slider
---

# Image Slider

The Image Slider component presents a folder of images or a CMS gallery as a touch-friendly slider. It supports autoplay, slide or fade transitions, multiple visible slides, arrows, and pagination dots.

### Supported Content and File Types

Use an image folder from Resources or a CMS gallery field. The images in the selected source become slides automatically.

### How to Use Image Slider

You’ll find Image Slider under **Media** in the Components list.

1. Drag **Image Slider** onto the page.
2. Choose Resource or CMS as the source.
3. Select the image folder or CMS field.
4. Configure playback, transition, and visible slides.
5. Choose the image ratio and style the pagination controls.

### Component Settings

#### Resources

**Type**

* **Resource** — Uses an image folder from Resources. This is the default.
* **CMS** — Uses a CMS Gallery field or a custom field.

For Resource, select **Images**. For CMS, choose Gallery or Custom under **Field**. When Custom is selected, enter the field name; the default is `custom_field`.

#### Slides

**Auto Play** is off by default. When enabled:

* **Interval** sets the time between changes in milliseconds and defaults to 3000.
* **Pause on Hover** pauses playback while the pointer is over the slider. It is off by default.

**Transition** chooses Slide or Fade. The default is Slide.

**Duration** sets the transition time in milliseconds and defaults to 500.

**Visible Slides** is available for Slide transitions, ranges from 1 to 12, and defaults to 1.

**Padding** controls space around the slider and defaults to theme spacing 2 on every side.

#### Images

**Aspect Ratio** offers Auto, Square, Landscape, Portrait, or Custom. Auto is the default. Custom reveals a ratio field, which defaults to `5/7`.

**Radius** and **Shadow** style each image.

#### Pagination

**Arrows** are enabled by default. Set their Size, Radius, and Normal or Hover background and icon colours.

**Dots** are enabled by default. Set their Size, Spacing, normal Color, and Active Color.

### Accessibility

Use meaningful image metadata in Resources or your CMS. Do not rely on autoplay to communicate essential information, and keep arrows and dots visible against every slide.

### Tips and Best Practices

* **Use consistent image dimensions:** Similar source ratios reduce cropping surprises.
* **Pause interactive sliders:** Enable Pause on Hover when autoplay is active.
* **Tune visible slides responsively:** Show fewer slides on narrow screens.

### Related Components

* [Gallery](gallery.md) — Displays a complete image grid with a lightbox.
* [Content Slider](content-slider.md) — Slides any combination of Elements components.
