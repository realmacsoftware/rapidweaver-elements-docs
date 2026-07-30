---
description: Scale, rotate, move, and skew components
---

# Transforms

Transforms change a component’s visual position, scale, rotation, or skew without changing the space reserved for it in the document layout.

{% embed url="https://youtu.be/BFDklORPBHA" %}

### Type

**Type** is not responsive and defaults to None.

* **None** — Applies no transform classes.
* **Static** — Applies one set of transform values.
* **Hover** — Reveals Over and Start/End state controls.

### Hover Over and State

For Hover, **Over** defaults to Self. It can respond to Self, Parent, Container, Grid, Flex, or Custom ID.

Custom ID reveals a blank **ID** field. Enter the raw ancestor ID without `#` or `group/`.

**State** defaults to Start:

* **Start** — The resting transform.
* **End** — The transform applied while the target is hovered.

### Origin

**Origin** sets the point around which scale, rotation, and skew occur. It defaults to Centre and offers Centre, each side, and each corner.

### Transform Settings

Static and each Hover state provide:

* **Scale** — Defaults to 100%. Values below 100 shrink; values above 100 enlarge.
* **Rotate** — Defaults to 0 degrees and accepts positive or negative values.
* **Translate → Horizontal** — Defaults to `0px`.
* **Translate → Vertical** — Defaults to `0px`.
* **Skew → Horizontal** — Defaults to 0 degrees.
* **Skew → Vertical** — Defaults to 0 degrees.

Translate accepts valid CSS lengths such as `12px`, `1rem`, `10%`, or `-2vw`.

{% hint style="warning" %}
Transforms do not move neighbouring components. A translated or scaled component can overlap other content or extend beyond the viewport.
{% endhint %}

### Transitions

Add a [Transition](transitions.md) to animate Hover transforms. Transforms usually work best with Apply to set to Transforms or Most Common.

### Custom ID Hover Groups

Container, Grid, and Flex automatically create the required hover group when an Advanced ID is set. Other parents must render the matching `group/your-id` class.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-24 at 12 .08.31@2x.png" alt="Transform controls for origin, scale, rotate, translate, and skew"><figcaption><p>Transforms can be static or have separate Start and End values.</p></figcaption></figure>
