---
description: Create ordered or unordered lists with styled markers and text
---

# List

The List component creates an editable ordered or unordered list. It provides direct control over the number of items, marker style, spacing, and text appearance.

### How to Use List

You’ll find List under **Content** in the Components list.

1. Drag **List** onto the page.
2. Choose Ordered or Unordered.
3. Set the number of items.
4. Edit the list text directly on the page.
5. Style the markers, spacing, and item text.

### Component Settings

#### List

**Type**

* **Unordered** — Creates a bulleted list. This is the default.
* **Ordered** — Creates a numbered list.

**Items** sets the number of editable list entries and defaults to 3.

**List Style Type** chooses None, Disc, Decimal, Circle, Square, Lower Alpha, Upper Alpha, Lower Roman, or Upper Roman. The default is Disc.

**Size** sets the marker size and defaults to 16.

**Position**

* **Inside** — Places markers inside the text block.
* **Outside** — Places markers outside the text block. This is the default.

**Marker Color** defaults to Text 50.

**Gap** sets space between items and defaults to theme spacing 2. **Padding** sets the inner spacing of each item and defaults to 0 on every side.

#### Item Text

Set the item text colour, opacity, font, size, weight, letter spacing, line height, case, italic, underline, and other available text styles.

### Accessibility

Choose Ordered when sequence matters and Unordered when it does not. Do not imitate a list with separate Text components, because the List component provides meaningful structure for assistive technologies.

### Related Components

* [Text](text.md) — Creates headings, paragraphs, labels, and short text blocks.
* [Typography](typography.md) — Styles longer structured content as one block.

{% include "../../.gitbook/includes/common-controls.md" %}
