---
description: A highly customisable navigational tree menu
---

# Tree

The Tree component builds a multi-level navigation from your site pages. It’s ideal for sidebars, documentation-style tables of contents, and any nested menu where visitors can expand and collapse sections while preserving your site structure.

### Tree Settings

{% columns %}
{% column width="50%" %}
#### Pages & Levels
- **Pages**: show All, just the **Active Page**, or a **Selected Page** branch.
- **Levels**: Auto depth or Manual with a level limit.
- **Preview Sub Menus**: show nested items while editing.
- **Open & Close**: set expand/collapse animation duration (ms).

{% hint style="success" %}
Tip: For large sites, use Manual depth to keep the menu easy to scan.
{% endhint %}

#### Icons
- Default chevron or your own SVG resource.
- Set icon size.
- Place at the start or end of each item.

#### Top Level
- Toggle page icons; set their size and spacing.
- Padding/gap controls.
- Font, weight, letter spacing, line height.
- Colors for normal/hover/active, background/opacity, radius.
{% endcolumn %}

{% column width="50%" %}
#### Second Level
- Indent and item spacing.
- Border width/color/opacity.
- Padding, fonts, text size/weight/spacing/line height.
- Colors for normal/hover/active; optional radius.

#### Third+ Levels
- Extra indent and spacing for deeper items.
- Border options.
- Padding, fonts, text and hover colors, radius as needed.

{% hint style="info" %}
Keep styling consistent across levels to avoid visual noise.
{% endhint %}
{% endcolumn %}
{% endcolumns %}

### Keyboard & accessibility
- Arrow keys move focus up/down; Home/End jump to first/last item.
- Enter or Space toggles the current branch.
- Uses ARIA tree roles and roving tabindex for screen readers.
- Open/closed state can persist in the browser (local storage) when enabled.

### Quick recipes
- **Basic sidebar**: Pages = All, Depth = Auto, default chevrons, animation 200ms.
- **Focused doc TOC**: Pages = Active Page, Depth = Manual (2), Preview Sub Menus on, animation 150ms.
- **Branded menu**: custom SVG icon at end, brand text/hover colors, top-level page icons on; deeper levels with simple text styling.
