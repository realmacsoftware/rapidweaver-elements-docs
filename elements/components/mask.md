---
description: Reveal wrapped content through SVG, edge, linear, or radial masks
---

# Mask

The Mask component clips its child content with an SVG or a configurable gradient. Use it to create shaped images, soft fades, or decorative edge treatments without editing the original content.

### How to Use Mask

You’ll find Mask under **Media** in the Components list.

1. Drag **Mask** onto the page.
2. Place the content to be masked inside it.
3. Choose SVG, Edge, Linear, or Radial under **Mask → Type**.
4. Configure the controls shown for that mask type.
5. Preview the result at each breakpoint.

### Component Settings

#### Mask

**Type**

* **None** — Applies no mask. This is the default.
* **SVG** — Uses an SVG resource as the mask.
* **Edge** — Fades one or more edges.
* **Linear** — Creates a straight gradient mask.
* **Radial** — Creates a circular or elliptical gradient mask.

**SVG**

* **SVG** — Selects the mask resource.
* **Mode** — Uses Alpha or Luminance. Alpha is the default.
* **Size** — Offers Auto, Contain, Cover, or Custom. Contain is the default.
* **Custom Size** — Appears for Custom and defaults to `100% 100%`.
* **Position** — Anchors the mask to the centre, an edge, or a corner. Centre is the default.
* **Repeat** — Offers No Repeat, Repeat, Horizontal, Vertical, Round, or Space. No Repeat is the default.

Opaque areas of the SVG reveal the wrapped content.

**Edge**

Choose Top, Right, Bottom, Left, Horizontal, or Vertical under **Side**. Bottom is the default. **From** and **To** set the fade range and default to 75% and 100%.

**Linear**

**Angle** defaults to 45°. **From** and **To** set the fade range and default to 10% and 90%.

**Radial**

**Size** offers Full, Closest Side, Closest Corner, Farthest Side, or Farthest Corner. Full is the default. **Position** defaults to Centre. **From** and **To** default to 70% and 100%.

### Accessibility

Masking should be decorative. Do not hide text or controls that visitors need to understand or operate the page.

### Tips and Best Practices

* **Use simple SVGs:** Clear black or opaque shapes produce predictable masks.
* **Check responsive crops:** Position and sizing may need different values at smaller breakpoints.
* **Keep controls visible:** Avoid masking interactive content near its hit area.

### Related Components

* [Image](image.md) — Includes a simpler SVG mask option for a single image.
* [SVG](svg.md) — Displays and styles vector artwork directly.

{% include "../../.gitbook/includes/common-controls.md" %}
