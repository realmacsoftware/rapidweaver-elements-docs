---
description: Set border style, colour, opacity, width, radius, and hover states
---

# Borders

Borders draw an outline around a component and can also round its corners. The shared control supports Static borders and animated Start/End states.

{% embed url="https://youtu.be/PaWL7Vieoh8?si=Y56iftuks4qwy6z1" %}

### Type

**Type** is not responsive and normally defaults to None.

* **None** — Applies no border classes.
* **Static** — Applies one border style.
* **Hover** — Reveals Start and End states.

Input-style controls use a specialised border that defaults to Static.

### State

**State** appears for Hover and defaults to Start.

* **Start** — The resting border.
* **End** — The border shown while the component itself is hovered.

Unlike Effects, Filters, and Transforms, the shared Borders control does not provide a separate Hover Over target.

### Style

**Style** defaults to Solid.

* **Solid** — Draws one continuous line.
* **Dashed** — Draws a sequence of dashes.
* **Dotted** — Draws a sequence of dots.

### Colour and Opacity

**Color** uses Theme Studio colours and normally defaults to Surface 500.

**Opacity** ranges from 0–100% and defaults to 100%.

### Width

**Width** controls Top, Right, Bottom, and Left border thickness. Link opposite sides for symmetrical borders or set them independently.

The general and Container variants default to 0 on every side. Input borders use the Theme Default width in their initial Static state.

### Radius

**Radius** controls the four corners. Link corners for one radius or set them independently.

The general variant defaults to the Theme Default radius. Container and Input variants default to None.

{% hint style="info" %}
A radius can clip a visible background only when the component’s overflow and rendering structure support it. If child content extends outside rounded corners, set [Layout → Overflow](layout.md#overflow) to Hidden.
{% endhint %}

### Hover Borders

Configure Start and End, then add a [Transition](transitions.md). Select Colors or Most Common to animate colour; width and radius animation may require All.

## Border UI in Elements

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-28 at 12 .03.54@2x.png" alt="Border controls for type, style, colour, width, and radius"><figcaption><p>Border controls support separate sides, corners, and hover states.</p></figcaption></figure>
