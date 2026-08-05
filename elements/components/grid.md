---
description: Build responsive two-dimensional layouts with CSS Grid
---

# Grid

The Grid component creates responsive layouts with defined columns and rows. It is ideal when content needs to align in two dimensions, such as card grids, galleries, feature comparisons, and structured page sections.

{% embed url="https://youtu.be/BFIvsNwJT7k" %}

👉🏻 [Open the Grid Project in Elements](elementsapp://downloadDocument/sJeeTVNqG8Er) that was used in this video.

### How to Use Grid

You’ll find Grid under **Layout** in the Components list.

1. Drag **Grid** onto the page.
2. Add Containers or other components to the grid.
3. Set the number of columns and rows.
4. Adjust horizontal and vertical gaps.
5. Select a child Container and set it to act as a Grid Item when it should span specific columns or rows.

{% hint style="info" %}
A newly added Grid may not look divided until it contains child components. Enable **Preview Columns** while editing to make the structure easier to see.
{% endhint %}

### Component Settings

#### Tags

Add tag titles when the Grid itself should be controlled by Filter or Filter Tags.

#### Filter

Enable filtering to make the Grid a filterable item. Choose parent or custom grouping and a Dim, Zoom Out, or Slide transition.

#### Columns & Rows

**Preview Columns** displays the grid structure in Edit mode. It does not affect the published page.

**Horizontal Gap** and **Vertical Gap** set spacing between cells. Both default to theme spacing 2.

**Columns** sets between 1 and 12 columns and defaults to 4.

**Rows** can be Auto or a fixed value from 1 to 12. The default is Auto.

#### Grid Alignment

**Auto Flow**

* **Row** — Places items by row. This is the default.
* **Column** — Places items by column.
* **Dense** — Attempts to fill earlier gaps.
* **Row Dense** and **Column Dense** — Combine a direction with dense placement.

**Auto Cols** and **Auto Rows** size automatically created tracks. Options are None, Auto, Min Content, Max Content, and 1 Fr.

**Justify Content** and **Align Content** position the grid tracks within the component. **Justify Items** and **Align Items** position children inside their grid areas.

#### Link

The Link group can make the whole Grid clickable. Avoid using it when the Grid contains its own links or buttons.

### Tips and Best Practices

* **Start with fewer columns:** Four columns with one-column items is easier to manage than twelve columns unless you need finer spans.
* **Use child spans deliberately:** Set Containers to Grid Item only when they need explicit column or row placement.
* **Review every breakpoint:** Reduce column counts on narrow screens to keep content readable.

### Related Components

* [Flex](flex.md) — Better suited to a single row or column.
* [Container](container.md) — Can be configured as a Grid Item and span multiple tracks.

{% include "../../.gitbook/includes/common-controls.md" %}
