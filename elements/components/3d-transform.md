---
description: Create perspective, depth, rotation, and mouse-driven 3D effects
---

# 3D Transform

The 3D Transform component wraps other components and gives them depth, perspective, and three-dimensional movement. Use it for tilting cards, rotating artwork, creating hover interactions, or making content respond to the visitor’s pointer.

### How to Use 3D Transform

You’ll find 3D Transform under **Interactive** in the Components list.

1. Drag **3D Transform** onto the page.
2. Place the component you want to transform inside its drop zone.
3. In **3D**, choose Static, Hover, or Mouse.
4. Set the perspective and the starting transform values.
5. For Hover or Mouse, switch **State** to End and set the destination values.
6. Preview the page in a browser to test the interaction.

### Component Settings

#### Transforms

These are the standard two-dimensional transform controls applied before the 3D effect.

**Type**

* **None** — Applies no transform. This is the default.
* **Static** — Applies one fixed transform.
* **Hover** — Animates between Start and End values when the selected element is hovered.

For Hover transforms, **Over** chooses the trigger: Self, Parent, Container, Grid, Flex, or Custom ID. When using Custom ID, enter the ID of the element that should trigger the effect.

**Origin** sets the pivot point. **Scale** defaults to 100%, **Rotate** to 0°, Translate to `0px`, and both Skew values to 0°. Hover mode provides separate Start and End values.

#### 3D

**Type**

* **None** — Disables 3D transforms. This is the default.
* **Static** — Applies a fixed 3D transform.
* **Hover** — Animates between Start and End values on hover.
* **Mouse** — Changes the transform in response to pointer movement.

For Hover and Mouse, **Over** selects Self, Parent, Container, Grid, Flex, or Custom ID as the trigger.

**Perspective**

* **Distance** — Controls the strength of perspective: Dramatic, Near, Normal, Midrange, Distant, or None. The default is Normal.
* **Origin** — Sets the viewpoint from Center or any edge or corner. The default is Center.

**Backface**

Enable **Hide** to prevent the reverse side of rotated content from showing. It is off by default.

**Transform Values**

* **X** and **Y** rotate the content around the horizontal and vertical axes. Both default to 0°.
* **Scale Z** controls depth scaling and defaults to 100%.
* **Depth** moves the content towards or away from the viewer and defaults to `0px`.

Hover and Mouse modes provide separate Start and End values.

#### Transitions

Transitions control how quickly Hover and Mouse states change. Set the animated property, easing curve, duration, and delay in the standard Transitions controls.

### Accessibility

Keep important content readable without the effect. Avoid large or rapid pointer-driven movement, and provide enough contrast when a transform changes the component’s appearance.

### Tips and Best Practices

* **Start subtly:** Small rotations and modest perspective usually feel more natural.
* **Test the backface:** Enable Backface Hide when content looks mirrored during a rotation.
* **Preview in a browser:** Mouse tracking and hover behaviour are best tested outside Edit mode.

### Related Components

* [Reveal](reveal.md) — Animates content as it enters the viewport.
* [Container](container.md) — Groups and styles the content placed inside a 3D Transform.

{% include "../../.gitbook/includes/common-controls (1).md" %}
