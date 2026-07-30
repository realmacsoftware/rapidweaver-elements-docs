---
description: Organise related content into selectable tab panels
---

# Tabs

The Tabs component displays one content panel at a time while keeping related sections easy to reach. Each tab has a title, optional SVG icon, and content drop zone.

{% hint style="info" %}
All tab content is loaded with the page, so it remains available to search engines and assistive technologies.
{% endhint %}

### How to Use Tabs

You’ll find Tabs under **Interactive** in the Components list.

1. Drag **Tabs** onto the page.
2. Add items to the **Tabs** collection.
3. Give each item a Title and optional Icon.
4. Use **Active Tab** to select the panel you are editing.
5. Choose the default active tab and style the list, buttons, titles, icons, and content.

### Component Settings

#### Settings

**Tabs** adds, removes, and reorders tab items. Each collection item has a Title and Icon.

**Default Active Tab** sets the initially selected tab and defaults to 1.

**Active Tab** selects the tab shown in Edit mode and also defaults to 1.

#### Tab List

**Alignment** offers Start, Centre, or End and defaults to Start.

**Gap** defaults to theme spacing 1 and **Padding** to 0.

**Background** defaults to None and **Border Radius** to None.

#### Tab Button

Use **State** to edit Inactive, Active, and Hover styles. Each state has Background, Text Color, Shadow, Border Width, Border Color, and Border Radius.

Defaults:

* **Inactive** — Surface 100 background, Text 50, no shadow or border, Medium radius.
* **Active** — Brand 500 background, Surface 50 text, no shadow or border, Brand 500 border colour, Medium radius.
* **Hover** — Surface 300 background, Text 50, no shadow or border, Surface 300 border colour, Medium radius.

**Padding** defaults to theme spacing 2 vertically and 4 horizontally.

#### Tab Title

Font defaults to Body.

Use **State** to edit Inactive, Active, and Hover Size, Weight, Spacing, Line Height, and Underline. Size defaults to Base for every state. Weights default to 400, 500, and 400. Spacing and line height default to Normal, and Underline is off.

#### Tab Icon

**Show Icon** is enabled by default.

**Position** offers Left, Right, or Top and defaults to Left. **Gap** defaults to theme spacing 2.

**Remove Attributes** controls whether Size, Fill, Stroke, and Styles are removed from each SVG. All four are enabled by default.

Use **State** to edit Inactive, Active, and Hover icon styles:

* **Size** — Defaults to `20px`.
* **Fill Color and Opacity** — Defaults to Text 50 for Inactive/Hover, Surface 50 for Active, and 100% opacity.
* **Stroke Color, Opacity, and Width** — Defaults to None, 100%, and 0.

#### Tab Content

Set Padding, Background, Border Width, Border Color, and Border Radius. Defaults are theme spacing 4, no background or border, Surface 200 border colour, and no radius.

#### Tab Content Above

**Show** is off by default. When enabled, it creates an additional shared area above the active tab content and reveals its Padding, Background, Border Width, Border Color, and Border Radius controls.

Defaults match Tab Content.

### Accessibility

Use short, descriptive titles and keep the active, hover, and keyboard focus states distinct. Do not use icons without text unless their meaning is unmistakable.

### Tips and Best Practices

* **Keep the set small:** Too many tabs become difficult to scan on narrow screens.
* **Use parallel content:** Tabs work best for sections at the same conceptual level.
* **Check icon attributes:** Disable only the Remove Attributes switches needed to preserve intentional SVG styling.

### Related Components

* [Accordion](accordion.md) — Better for vertically stacked questions or sections.
* [Content Slider](content-slider.md) — Adds sequential or automatic playback.

{% include "../../.gitbook/includes/common-controls.md" %}
