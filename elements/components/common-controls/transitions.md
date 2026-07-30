---
description: Control which properties animate and set their timing
---

# Transitions

Transitions control how quickly a component moves between states created by Backgrounds, Borders, Effects, Filters, Transforms, and other hover-aware controls.

{% embed url="https://youtu.be/tg2k4ZcFeQg" %}

### Apply to

**Apply to** defaults to All.

| Option | Animated properties |
| --- | --- |
| None | Disables transitions. |
| All | Animates every property that supports CSS transitions. |
| Most Common | Animates colour, background, border colour, text decoration, fill, stroke, opacity, shadows, transforms, filters, and backdrop filters. |
| Colors | Animates colour-related properties only. |
| Opacity | Animates opacity only. |
| Shadows | Animates box and text shadows only. |
| Transforms | Animates transform properties only. |

Use Most Common when All causes an unrelated layout property to animate.

### Function

**Function** controls the timing curve and defaults to Ease-in-out.

* **Custom** — Reveals a Cubic Bezier field.
* **Linear** — Moves at a constant rate.
* **Ease-in** — Starts slowly and accelerates.
* **Ease-out** — Starts quickly and decelerates.
* **Ease-in-out** — Starts and ends slowly.

#### Custom Timing Functions

The **Cubic Bezier** field accepts four comma-separated values: `x1,y1,x2,y2`. It defaults to:

```text
0.95,0.05,0.795,0.035
```

The x values must remain between 0 and 1. The y values may extend below 0 or above 1 to create anticipation or overshoot.

This second example overshoots before settling:

```text
0.21,1,1,1.53
```

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-17 at 10 .31.23.gif" alt="A fast custom cubic-bezier transition"><figcaption><p>The default custom curve starts quickly and ends abruptly.</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-17 at 10 .28.15.gif" alt="A custom cubic-bezier transition that overshoots"><figcaption><p>Values above 1 on the y-axis can create overshoot.</p></figcaption></figure>

Use [Cubic-Bezier.com](https://cubic-bezier.com) to experiment visually.

### Timing

**Duration** is measured in milliseconds and defaults to 300. For example:

* `150` feels quick and responsive.
* `300` is the default general-purpose transition.
* `1000` lasts one second.

**Delay** is measured in milliseconds and defaults to 0.

Function, Duration, and Delay are hidden when Apply to is None.

{% hint style="info" %}
Configure the Start and End states first, then adjust the transition. A transition cannot create a visual change when both states use the same values.
{% endhint %}

## Transitions UI in Elements

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-17 at 9 .52.22@2x.png" alt="Transition controls for property, function, duration, and delay"><figcaption><p>Transition controls determine what animates and how long the change takes.</p></figcaption></figure>
