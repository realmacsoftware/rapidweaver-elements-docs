---
description: Add responsive margin and padding to components
---

# Spacing

Spacing controls the space outside and inside a component:

* **Margin** creates space outside the component’s border.
* **Padding** creates space between its content and border.

{% embed url="https://youtu.be/8xS_OMqpw4U" %}

### Enable

The general Spacing control is disabled by default. Enabling **Margin & Padding** reveals both diagrams, with every side set to 0.

Some controls use specialised defaults:

| Variant | Enabled | Margin | Padding |
| --- | --- | --- | --- |
| General | No | 0 on every side | 0 on every side |
| Container | Yes | Top 0, Right Auto, Bottom 0, Left Auto | 0 on every side |
| Button | Yes | Top 0, Right Auto, Bottom 0, Left Auto | 2 vertically and 3.5 horizontally |
| Input | Yes | 0 on every side | 2 vertically and 3.5 horizontally |

Disabling Spacing removes its margin and padding classes rather than setting them to 0.

### Using the Spacing Control

The Theme/Manual button switches between Theme Spacing values and arbitrary CSS values. Drag a manual value to adjust it; hold Shift while dragging for finer increments.

The links between opposite sides control whether vertical or horizontal values change together.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-16 at 3 .05.02@2x.png" alt="Spacing controls with margin and padding diagrams"><figcaption><p>Margin surrounds the component; padding sits inside it.</p></figcaption></figure>

### Margin

Set Top, Right, Bottom, and Left independently or link opposite sides. Manual values can be negative when an intentional overlap is required.

**Auto** tells the browser to absorb available space on that side. Common horizontal combinations are:

* **Left Auto + Right Auto** — Centres a component with a constrained width.
* **Left 0 + Right Auto** — Keeps it at the start.
* **Left Auto + Right 0** — Pushes it to the end.

{% hint style="warning" %}
Auto margins can override the alignment and gap set by a Flex or Grid parent. For children inside Flex or Grid, set all margins to 0 unless the Auto margin is an intentional item-level override.
{% endhint %}

### Padding

Set Top, Right, Bottom, and Left independently or link opposite sides. Padding expands the area occupied by a background, border, or rounded corner and keeps content away from those edges.

Useful starting points include:

* Equal padding on every side for cards and panels.
* Larger vertical than horizontal padding for banners.
* Compact vertical and horizontal padding for buttons and inputs.

### Responsive Spacing

Margin and padding values can change by breakpoint. Start with the smallest/Base layout, then override only the sides that need to change at larger breakpoints.
