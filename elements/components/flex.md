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

Add tags when this Flex should be controlled by a [Filter](filter.md) or [Filter Tags](filter-tags.md) component. Each collection item contains one tag title. Tags on their own do not make the Flex filterable — you must also switch on **Filter → Enable** and put the Flex in the same group as the Filter or Filter Tags component.

#### Filter

Enable filtering to make the Flex a filterable item. Use its parent as the group or provide a custom Group ID, then choose the Dim, Zoom Out, or Slide transition.

#### Flexbox Settings

**Direction** controls the main axis. Choose Column (the default), Column Reverse, Row, or Row Reverse. A new Flex stacks its children vertically until you switch it to Row.

**Wrap Items**

* **No Wrap** — Keeps all children on one line. This is the default.
* **Wrap** — Moves items onto additional lines when space runs out.
* **Wrap Reverse** — Wraps additional lines in the opposite cross-axis direction.

**Gap**

Horizontal and Vertical gaps independently control spacing between items. Both default to theme spacing 2.

**Align**

**Content** distributes the lines of a wrapped container along the cross axis. It only
has an effect when Wrap Items is set to Wrap or Wrap Reverse and the items occupy more
than one line. Defaults to Normal.

* **Normal** — Lines keep their default position.
* **Start**, **End**, **Center** — Packs the lines at the start, end, or centre of the cross axis.
* **Between**, **Around**, **Evenly** — Spreads the spare space between, around, or evenly among the lines.
* **Stretch** — Lines grow to fill the cross axis.
* **Baseline** — Aligns the lines on their first baseline.

**Items** aligns each child within its line, on the cross axis. Defaults to Normal.

* **Normal** — Children behave as if Stretch were set, unless they have a size of their own.
* **Start**, **End**, **Center** — Aligns children at the start, end, or centre of the cross axis.
* **Stretch** — Children fill the cross axis of the line.
* **Baseline** — Aligns children on their text baseline, which is useful for mixed type sizes.

**Justify**

**Content** distributes the children along the main axis — the axis set by Direction.
Defaults to Normal.

* **Normal** — Children keep their default position.
* **Start**, **End**, **Center** — Packs the children at the start, end, or centre of the main axis.
* **Between**, **Around**, **Evenly** — Spreads the spare space between, around, or evenly among the children.
* **Stretch** — Children grow to fill the main axis where they have no fixed size.

**Items** maps to the CSS `justify-items` property, which sets the default inline-axis
alignment of each child within its own area. It is honoured by grid layouts; in a Flex
container the main-axis distribution comes from Justify Content instead. Use
[Grid](grid.md) when you need per-item justification. Defaults to Normal. Options are
Normal, Start, End, Center, and Stretch.

#### Link

The Link group can make the whole Flex clickable. Avoid wrapping multiple interactive child controls inside one link. When a link destination is set, Flex renders as an `<a>` element. This replaces whatever is chosen under **Advanced → HTML Tag** — clear the link if you need a different wrapper tag.

### Tips and Best Practices

* **Use Row for horizontal groups:** It is ideal for buttons, badges, and navigation items.
* **Use Column for stacks:** It gives vertical layouts consistent gap control.
* **Reset child auto margins:** Auto margins on Buttons can override the Flex Gap and Justify settings.

### Related Components

* [Grid](grid.md) — Creates two-dimensional row-and-column layouts.
* [Container](container.md) — Groups content and can act as a Flex item.

{% include "../../.gitbook/includes/common-controls.md" %}
