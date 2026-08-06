---
description: Animate components as they enter or leave the viewport
---

# Reveal

The Reveal component animates its child content in response to scrolling. Choose a fade, slide, zoom, light-speed, or rotation effect, then control when and how the animation plays.

{% embed url="https://www.youtube.com/watch?v=7zZiIZtXf9c" %}

### How to Use Reveal

You’ll find Reveal under **Animation** in the Components list.

1. Drag **Reveal** onto the page.
2. Place the component you want to animate inside it.
3. Choose Smooth or Scrub mode.
4. Select the animation, direction, and trigger points.
5. Set timing values and preview the page while scrolling.

### Component Settings

#### Reveal

**Mode**

* **Smooth** — Plays the animation after its trigger is reached. This is the default.
* **Scrub** — Links animation progress to the page’s scroll position between Start and End.

**Animation** offers Fade, Slide, Zoom, Light Speed, or Rotate. Fade is the default.

**Direction** can be Up, Down, Left, or Right and defaults to Up.

**Distance** sets how far the content travels and defaults to `200px`. Use any valid CSS length.

**Degrees** appears for Rotate and defaults to 90°.

**Trigger**

* **Play** — When the animation runs. **Once on Enter** plays it the first time the content enters the viewport and never again; **Always on Enter** replays it each time the content scrolls into view from below; **Enter and Exit** (the default) also plays a matching exit animation when the content leaves, and replays on re-entry in either direction.
* **Start** / **End** — Where the animation is triggered, measured against the top edge of the Reveal content: **Entering Screen** as it reaches the bottom of the viewport, **Middle of Screen** as it reaches the centre, and **Exiting Screen** as it reaches the top. Start defaults to Entering Screen; End defaults to Exiting Screen. In Scrub mode the animation progresses between the Start and End positions.

**Timing**

* **Easing** — Offers Linear, Power0–Power4, Sine, Circ, Expo, Back, Elastic, or Bounce. The default is Power1.
* **Duration** — Available in Smooth mode and defaults to 500 milliseconds.
* **Delay** — Available in Smooth mode and defaults to 0 milliseconds.

**Markers** displays the Start and End trigger positions for debugging. It is off by default; disable it before publishing.

#### Flexbox and Grid

Set the Reveal component to act as a Grid Item or Flex Item when its parent layout needs explicit span, order, alignment, or sizing controls.

### Accessibility

Keep movement subtle and never make the animation the only way to discover essential content. Check that the page remains understandable when the visitor prefers reduced motion.

### Troubleshooting

#### The page scrolls horizontally on iPhone

A Reveal animation can temporarily extend beyond the viewport. Select the parent Container and set **Layout → Overflow** to Hidden so the animated content is clipped to the section.

### Related Components

* [3D Transform](3d-transform.md) — Creates hover and pointer-driven depth effects.
* [Container](container.md) — Wraps and clips Reveal animations.

{% include "../../.gitbook/includes/common-controls.md" %}
