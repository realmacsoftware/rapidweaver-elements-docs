---
description: Present custom content in an autoplaying or visitor-controlled slider
---

# Content Slider

The Content Slider component displays a collection of slides containing any Elements components. It is useful for testimonials, feature panels, announcements, or other content that visitors can move through with arrows or dots.

### How to Use Content Slider

You’ll find Content Slider under **Interactive** in the Components list.

1. Drag **Content Slider** onto the page.
2. Add items to the **Slides** collection.
3. Select a slide in **Active Slide** to edit its drop zone.
4. Choose the transition and autoplay behaviour.
5. Style the arrows, dots, background, and borders.

### Component Settings

#### Slides

**Slides** adds, removes, and reorders the slides. Each collection item creates a drop zone that can contain other components.

**Active Slide** chooses which numbered slide is displayed in Edit mode. It defaults to 1 and does not change the slide visitors initially see.

#### Playback

**Effect** controls the transition:

* **Slide** — Moves horizontally between slides. This is the default.
* **Fade** — Crossfades between slides.

**Auto Play** is enabled by default. When enabled, **Interval** controls the delay between slides: 3, 5, 7, 10, or 15 seconds. The default is 5 seconds.

#### Navigation

**Arrows**

* **Show Arrows** — Displays previous and next controls. Enabled by default.
* **Size** — Sets the arrow button size. The default theme spacing value is 10.
* **Radius** — Sets the corner radius. The default is Full.
* **State** — Switches between Normal and Hover styling.
* **Background** and **Color** — Set the button and icon colours for the selected state.

**Dots**

* **Show Dots** — Displays pagination dots. Enabled by default.
* **Size** — Defaults to theme spacing 3.
* **Spacing** — Defaults to theme spacing 2.
* **State** — Switches between Normal and Active styling.
* **Color** and **Active Color** — Set the colours for inactive and current-slide dots.

#### Slide Collection

Each Slides collection item has a **Title** used to identify it in Elements. The default title is “Slide”.

### Accessibility

Do not place essential information in only one automatically advancing slide. Make sure controls have sufficient contrast, and allow visitors enough time to read each slide.

### Tips and Best Practices

* **Keep slide heights consistent:** Similar content lengths prevent distracting layout shifts.
* **Use measured autoplay:** Five to seven seconds is a comfortable starting interval for short content.
* **Check every slide:** Use Active Slide in Edit mode to review the complete collection.

### Related Components

* [Image Slider](image-slider.md) — A slider designed specifically for images.
* [Tabs](tabs.md) — Lets visitors choose content directly without automatic playback.

{% include "../../.gitbook/includes/common-controls (1).md" %}
