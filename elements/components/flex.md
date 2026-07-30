---
description: Arrange components in a responsive row or column with Flexbox
---

# Flex

The Flex component is a one-dimensional layout tool based on CSS Flexbox. It arranges child components in a row or column and gives you responsive control over direction, wrapping, spacing, and alignment.

{% embed url="https://youtu.be/zS3g9dL31Ac" %}

### How to Use Flex

You’ll find Flex under **Layout** in the Components list.

1. Drag **Flex** onto the page.
2. Add components to its drop zone.
3. Choose a row or column direction.
4. Set wrapping, gaps, alignment, and justification.
5. Adjust settings at each breakpoint as required.

### Component Settings

#### Tags

Add tags when this Flex should be controlled by a [Filter](filter.md) or [Filter Tags](filter-tags.md) component. Each collection item contains one tag title.

#### Filter

Enable filtering to make the Flex a filterable item. Use its parent as the group or provide a custom Group ID, then choose the Dim, Zoom Out, or Slide transition.

#### Flexbox Settings

**Direction** controls the main axis. Choose Row, Row Reverse, Column, or Column Reverse.

**Wrap Items**

* **No Wrap** — Keeps all children on one line. This is the default.
* **Wrap** — Moves items onto additional lines when space runs out.
* **Wrap Reverse** — Wraps additional lines in the opposite cross-axis direction.

**Gap**

Horizontal and Vertical gaps independently control spacing between items. Both default to theme spacing 2.

**Align**

* **Align Content** positions multiple wrapped lines on the cross axis.
* **Align Items** positions children within the current line.

**Justify**

* **Justify Content** distributes items along the main axis.
* **Justify Items** controls item justification where supported.

#### Link

The Link group can make the whole Flex clickable. Avoid wrapping multiple interactive child controls inside one link.

### Tips and Best Practices

* **Use Row for horizontal groups:** It is ideal for buttons, badges, and navigation items.
* **Use Column for stacks:** It gives vertical layouts consistent gap control.
* **Reset child auto margins:** Auto margins on Buttons can override the Flex Gap and Justify settings.

### Related Components

* [Grid](grid.md) — Creates two-dimensional row-and-column layouts.
* [Container](container.md) — Groups content and can act as a Flex item.

{% include "../../.gitbook/includes/common-controls.md" %}
