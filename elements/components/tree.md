---
description: Build expandable, multi-level navigation from your site pages
---

# Tree

The Tree component builds hierarchical navigation from your site structure. It is ideal for documentation sidebars, large section menus, and any nested navigation where visitors need to expand and collapse page groups.

### How to Use Tree

You’ll find Tree under **Navigation** in the Components list.

1. Drag **Tree** onto the page or into a sidebar.
2. Choose All, Active Page, or Selected Page as the source.
3. Set automatic or manual depth.
4. Select the submenu SVG and configure its placement.
5. Style top-level, second-level, and deeper menu items.
6. Preview submenus while editing, then test the complete tree in a browser.

### Component Settings

#### General

**Preview Sub Menus** displays all nested items in Edit mode. It is off by default.

**Use**

* **All** — Builds from the complete site hierarchy. This is the default.
* **Active Page** — Builds from children of the active page.
* **Selected Page** — Builds from children of the selected Page link.

**Depth** can be Auto or Manual. Auto is the default. Manual reveals **Show**, which defaults to 1 level.

**Duration** controls opening and closing in milliseconds and defaults to 200.

#### SVG Icon

**Icon** selects the submenu indicator SVG.

**Size** defaults to theme spacing 4.

**Placement** positions the icon at Start or End and defaults to End.

#### Top Level Pages

**Page Icon Display** is off by default. When enabled, Size defaults to theme spacing 5 and Spacing to 2.

Layout controls include item **Padding** and **Gap**; the gap defaults to theme spacing 2.

Font controls include Font, Size, Weight, Letter Spacing, and Line Height. Font defaults to Body and Size to Base.

**Radius** defaults to 0. Use **State** to edit Normal and Hover Text, Background, and background Opacity independently.

#### Second Level Menus

**Indent** defaults to theme spacing 3 and **Item Spacing** to 2.

Border controls set Size, Color, and Opacity. The default border width is 0, colour is Surface 200, and opacity is 100%.

#### Second Level Items

Set Padding, Font, Size, Weight, Letter Spacing, Line Height, and Radius. Use State to edit Normal and Hover Text, Background, and Opacity.

Normal background opacity defaults to 0%, keeping the background transparent.

#### Third+ Level Menus

**Indent** and **Item Spacing** both default to theme spacing 3. Border Size defaults to 0, Color to Surface 200, and Opacity to 100%.

#### Third+ Level Items

These repeat the second-level item controls for deeper pages: Padding, typography, Radius, and separate Normal and Hover Text, Background, and Opacity.

### Accessibility

Keep page names concise and make expanded, collapsed, active, hover, and keyboard focus states visually distinct. Use a familiar submenu icon and test every level with a keyboard.

### Tips and Best Practices

* **Limit visible depth:** Very deep trees can overwhelm visitors; show only the levels needed for the current section.
* **Use Preview for styling:** Turn it on while working, then test real expansion in a browser.
* **Differentiate hierarchy:** Use indentation, spacing, or text weight consistently between levels.

### Related Components

* [Menu](navigation-standard.md) — Provides primary responsive site navigation.
* [Breadcrumbs](breadcrumbs.md) — Shows the path to the current page.
* [Top Pages](top-pages.md) — Displays a flat list of top-level pages or folder contents.

{% include "../../.gitbook/includes/common-controls.md" %}
