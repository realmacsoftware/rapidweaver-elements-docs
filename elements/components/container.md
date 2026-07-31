---
description: Group, lay out, style, and link other components
---

# Container

The Container component is the primary wrapper for grouping related components. It controls content width and alignment, backgrounds, overlays, spacing, borders, links, filtering, and how the Container behaves inside Flex and Grid layouts.

{% hint style="info" %}
Project-wide container widths can be set for each breakpoint in [Theme Studio → Screens](../theme-studio/screens.md).
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=wpMW6ysKqKk" %}

### How to Use Container

You’ll find Container under **Layout** in the Components list.

1. Drag **Container** onto the page.
2. Add components to its drop zone.
3. Set the content width, height, alignment, and gap.
4. Add padding to create space inside the section and margin to position it externally.
5. Apply a background, overlay, border, or link if required.

### Component Settings

#### Tags and Filter

The **Tags** collection adds tag titles used by Filter and Filter Tags.

Enable **Filter** to make the Container a filterable item. Choose Parent or Custom grouping; Custom reveals a Group ID. The transition can be Dim, Zoom Out, or Slide.

#### Link

**To** can make the whole Container clickable. Do not use a Container link when it contains Buttons, links, form controls, or other interactive components.

#### Flexbox and Grid

**Type**

* **Default** — Uses normal layout behaviour.
* **Grid Item** — Exposes grid column, row, span, and placement controls.
* **Flex Item** — Exposes flex order, growth, shrink, basis, and self-alignment controls.

Standard and Advanced modes reveal the appropriate level of placement control. These settings apply only when the Container is inside the matching Grid or Flex parent.

#### Content Layout

**Width** offers Auto, Full, Screen, Breakpoint, or Theme Spacing. Breakpoint is the default. Theme Spacing reveals a value that defaults to 36.

**Height** offers the same modes and defaults to Auto. Its Theme Spacing value also defaults to 36.

**Align** controls the cross-axis position and **Justify** controls the main-axis position. Both offer Auto, Start, End, Centre, or Stretch and default to Centre.

**Gap** controls spacing between child components and defaults to 0.

#### Effects, Filters, and Transforms

Each group has a **To** setting:

* **Everything** — Applies to content and background. This is the default.
* **Background** — Applies only to the background layer.
* **Content** — Applies only to child content.

The remaining controls configure the selected effect, filter, or transform.

#### Background and Background Overlay

Background supports colour, image, gradient, SVG, and video styles where shown. Configure resources, colours, opacity, image positioning, gradient stops, or video options for the selected type.

Background Overlay adds a separate colour, gradient, image, or effect layer above the background and behind the content.

#### Advanced

**HTML Tag** changes the Container’s semantic wrapper. Choose an appropriate standard tag or enter a custom one.

The **Custom Attributes** collection adds Attribute and Value pairs to the Container’s HTML. Use valid attributes and avoid duplicating built-in controls such as ID and class.

### Tips and Best Practices

* **Use padding for internal space:** Margin separates the Container from surrounding components.
* **Use Auto margins deliberately:** Equal left and right Auto margins centre a fixed-width Container.
* **Keep structure meaningful:** Prefer semantic HTML tags when the Container represents a section, header, footer, or main region.
* **Apply one-off utility styles carefully:** For example, adding `blur-sm` under Advanced → CSS Classes blurs the Container and its contents. See the [Tailwind blur utilities](https://tailwindcss.com/docs/blur) and [Tailwind CSS documentation](https://tailwindcss.com/docs/).

### Related Components

* [Flex](flex.md) — Arranges children in a row or column.
* [Grid](grid.md) — Creates two-dimensional layouts.
* [Background](background.md) — Adds angled or fixed backgrounds.
* [Filter](filter.md) — Searches tagged Containers.

{% include "../../.gitbook/includes/common-controls.md" %}
