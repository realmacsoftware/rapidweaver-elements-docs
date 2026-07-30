---
description: Apply shadows, opacity, and hover effects
---

# Effects

Effects add a box shadow or change the opacity of a component. They can remain static or animate between Start and End states when a visitor hovers.

{% embed url="https://youtu.be/IljWfMjwW-Y" %}

### Type

**Type** is not responsive and defaults to None.

* **None** — Applies no Effect classes.
* **Static** — Applies one set of shadow and opacity values.
* **Hover** — Reveals Over and Start/End state controls.

### Hover Over

When Type is Hover, **Over** defaults to Self.

| Option | The End state is triggered when the visitor hovers over… |
| --- | --- |
| Self | This component. |
| Parent | Its direct parent. |
| Container | An ancestor Container. |
| Grid | An ancestor Grid. |
| Flex | An ancestor Flex. |
| Custom ID | The ancestor with the supplied ID. |

Custom ID reveals **ID**, which is blank by default. Enter the raw ID without a `#` or `group/` prefix.

### State

**State** appears for Hover and defaults to Start.

* **Start** — The normal, resting appearance.
* **End** — The appearance while the chosen target is hovered.

State changes which values you are editing; it does not force that state in the published page.

### Box Shadow

For Static and each Hover state:

* **Size** — Selects a Theme Studio shadow and defaults to Default.
* **Color** — Overrides the shadow colour and defaults to None.
* **Opacity** — Controls shadow-colour opacity from 0–100% and defaults to 100%.

### Opacity

The component **Opacity** ranges from 0–100% and defaults to 100% for Static and both Hover states.

{% hint style="info" %}
Add a [Transition](transitions.md) when using Hover. Without one, the Start and End values switch immediately.
{% endhint %}

### Custom ID Hover Groups

Container, Grid, and Flex automatically create the required hover group when an Advanced ID is set. For a different or custom parent, ensure it renders the matching `group/your-id` class.

## Effects UI in Elements

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-23 at 5 .37.01@2x.png" alt="Effects controls for type, hover state, shadow, and opacity"><figcaption><p>Effects can be static or respond to a hover target.</p></figcaption></figure>
