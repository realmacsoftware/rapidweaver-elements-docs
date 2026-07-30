---
description: Reveal links, actions, or custom content from a compact trigger
---

# Dropdown

The Dropdown component reveals custom content when a visitor interacts with its trigger. It is useful for navigation choices, action menus, and contextual information that should remain hidden until needed.

The trigger and panel are both drop zones, so you can build them from Text, Button, SVG, or other suitable components.

{% embed url="https://www.youtube.com/watch?v=izxsNWPrPe8" %}

### How to Use Dropdown

You’ll find Dropdown under **Interactive** in the Components list.

1. Drag **Dropdown** onto the page.
2. Add the visible trigger content to the trigger drop zone.
3. Add the hidden menu or content to the panel drop zone.
4. Enable **Panel → Show** while editing the panel.
5. Choose the panel placement and transition.
6. Disable Show and preview the interaction in a browser.

### Component Settings

#### Settings

**Show** displays the panel in Edit mode. It is off by default and does not force the panel open on the published page.

**Vertical** places the panel below or above the trigger. The default is Bottom.

**Horizontal** aligns the panel to the Left, Center, or Right of the trigger. The default is Center.

#### Transition

**Style** chooses None, Fade, Zoom, Slide Left, Slide Right, Slide Up, or Slide Down. The default is Fade.

**Duration** sets the animation length in milliseconds and defaults to 300.

### Accessibility

Use a clear, focusable trigger such as a Button. Keep interactive controls inside the panel keyboard accessible, and do not rely on hover alone to communicate essential information.

### Tips and Best Practices

* **Use Show only for editing:** Turn it off before testing the published interaction.
* **Check page edges:** Change Horizontal alignment when the panel would otherwise overflow the viewport.
* **Keep menus concise:** Large or complex content is usually better suited to a Modal.

### Related Components

* [Modal](modal.md) — Displays larger content in an overlay.
* [Menu](navigation-standard.md) — Builds navigation automatically from your site pages.
