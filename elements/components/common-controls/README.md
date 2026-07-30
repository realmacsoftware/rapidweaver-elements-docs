---
description: Learn the Inspector controls shared by built-in components
---

# Common Controls

Common Controls are reusable Inspector groups that behave consistently across built-in components. Learning them once makes it easier to size, position, style, animate, and link components throughout a project.

The available groups depend on the selected component. Some components use a specialised variant with different defaults—for example, Image starts at 100% width, while a general component starts at Auto.

{% hint style="info" %}
Many values are responsive. When a control supports breakpoints, set the Base value first and add overrides only where the design needs to change.
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody>
<tr><td>Link</td><td><a href="link.md">link.md</a></td></tr>
<tr><td>Layout</td><td><a href="layout.md">layout.md</a></td></tr>
<tr><td>Sizing</td><td><a href="sizing.md">sizing.md</a></td></tr>
<tr><td>Spacing</td><td><a href="spacing.md">spacing.md</a></td></tr>
<tr><td>Typography & Text Styles</td><td><a href="typography-and-text-styles.md">typography-and-text-styles.md</a></td></tr>
<tr><td>Backgrounds</td><td><a href="backgrounds.md">backgrounds.md</a></td></tr>
<tr><td>Transitions</td><td><a href="transitions.md">transitions.md</a></td></tr>
<tr><td>Effects</td><td><a href="effects.md">effects.md</a></td></tr>
<tr><td>Filters</td><td><a href="filters.md">filters.md</a></td></tr>
<tr><td>Transforms</td><td><a href="transforms.md">transforms.md</a></td></tr>
<tr><td>Borders</td><td><a href="borders.md">borders.md</a></td></tr>
<tr><td>Advanced</td><td><a href="advanced.md">advanced.md</a></td></tr>
</tbody></table>

### How Common Controls Work

* **Theme values** use colours, spacing, typography, shadows, and borders defined in Theme Studio.
* **Custom values** accept valid CSS values where the control provides a manual mode.
* **Responsive controls** can be overridden at different breakpoints.
* **State controls** let you edit Static, Start, End, Normal, Hover, or other states without changing the state visitors initially see.
* **Conditional controls** appear only after the related feature is enabled or a compatible Type or Style is selected.

Individual component pages document any specialised defaults or behaviour that differs from these shared guides.
