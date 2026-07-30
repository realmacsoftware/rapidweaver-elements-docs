---
description: Apply blur, brightness, saturation, shadow, and backdrop effects
---

# Filters

Filters change how a component and its contents are rendered. Use them for blur, brightness, saturation, drop shadows, and backdrop blur.

{% embed url="https://www.youtube.com/watch?v=wFKU85vhOEQ&list=PLlqV01jBZsjA6LyBb9uY-H7EtHjgO1HcR&index=1&pp=iAQB" %}

### Type

**Type** is not responsive and defaults to None.

* **None** — Applies no filter classes.
* **Static** — Applies one set of filter values.
* **Hover** — Reveals Over and Start/End state controls.

### Hover Over and State

For Hover, **Over** defaults to Self. It can respond to Self, Parent, Container, Grid, Flex, or Custom ID.

Custom ID reveals a blank **ID** field. Enter the raw ancestor ID without `#` or `group/`.

**State** defaults to Start:

* **Start** — The resting filters.
* **End** — The filters applied while the chosen target is hovered.

### Filters

Static and each Hover state provide:

* **Blur** — Defaults to 0 pixels.
* **Brightness** — Defaults to 100%. Lower values darken; higher values brighten.
* **Saturate** — Defaults to 100%. `0` removes colour; values above 100 increase saturation.
* **Drop Shadow** — Defaults to None and uses Theme Studio shadow values.

### Backdrop Filters

**Backdrop Blur** defaults to 0 pixels. It blurs content behind the component rather than the component itself.

Backdrop blur is easiest to see when the component has a transparent or semi-transparent [Background](backgrounds.md). A fully opaque background hides the content being blurred.

{% hint style="info" %}
Add a [Transition](transitions.md) for smooth Hover filters. Large blur and backdrop-blur values can be expensive to render, especially over video or animated content.
{% endhint %}

### Custom ID Hover Groups

Container, Grid, and Flex automatically create the required hover group when an Advanced ID is set. Other parents must render the matching `group/your-id` class.

## Filters UI in Elements

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-23 at 5 .30.10@2x.png" alt="Filter controls for blur, brightness, saturation, drop shadow, and backdrop blur"><figcaption><p>Filters can remain static or animate between hover states.</p></figcaption></figure>
