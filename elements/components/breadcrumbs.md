---
description: Show the current page’s position within the site hierarchy
---

# Breadcrumbs

The Breadcrumbs component builds a trail from the current page back through its parent pages. It helps visitors understand where they are and move to a higher level of the site.

### How to Use Breadcrumbs

You’ll find Breadcrumbs under **Navigation** in the Components list.

1. Drag **Breadcrumbs** onto a page or shared layout.
2. Choose whether to show the Home link.
3. Select an SVG separator and style its colour and size.
4. Configure mobile truncation, spacing, alignment, and text states.
5. Preview the component on pages at different levels of the site.

### Component Settings

#### Breadcrumbs

**Separator**

* **Icon** — Selects the SVG displayed between breadcrumb items.
* **Color** — Defaults to Text 400.
* **Size** — Defaults to theme spacing 4.

**Home Link**

**Show** is enabled by default. **Label** changes its text and defaults to “Home”.

**Truncate on Mobile**

**Enable** is on by default. On small screens, it shows only the direct parent and current page to keep the trail compact.

**Layout**

**Gap** controls item spacing and defaults to theme spacing 2. **Align** offers Start, Centre, or End and defaults to Centre.

**Font & Text Styles**

Font defaults to Body, Size to Small, Weight to 400, and letter spacing to Normal. Italic is off.

Use **State** to style Default and Active items independently. Each state provides Color, Opacity, and Underline controls.

### Accessibility

The current page is identified to assistive technologies automatically. Keep separators decorative, retain visible link states, and use a concise Home label.

### Related Components

* [Menu](navigation-standard.md) — Provides primary site navigation.
* [Tree](tree.md) — Shows expandable navigation across multiple levels.
* [Top Pages](top-pages.md) — Lists top-level pages or a folder’s contents.

{% include "../../.gitbook/includes/common-controls (1).md" %}
