---
description: Set component width, height, and responsive size constraints
---

# Sizing

Sizing controls the displayed width and height of a component. Values can come from Theme Spacing or use custom CSS units and functions.

{% embed url="https://youtu.be/cCSxBM194SQ" %}

### Width and Height

The general Sizing control defaults to **Auto** width and **Auto** height.

Container-style components use selection menus:

| Option | Behaviour |
| --- | --- |
| Auto | Lets content, the parent, and the browser determine the size. |
| Full | Uses the full size of the parent: 100% width or height. |
| Screen | Uses the viewport: 100vw width or 100vh height. |
| Breakpoint | Uses the configured Theme Studio breakpoint width. Available for container width. |
| Theme Spacing | Reveals a responsive Theme Spacing or custom value. |

Container-style Sizing defaults to **Full** width and **Auto** height. [Theme Studio → Screens](../../theme-studio/screens.md) controls Breakpoint widths.

{% hint style="info" %}
Auto is standard CSS auto sizing, not shrink-to-fit: a block-level component with Auto width fills the available width of its parent. To centre a component that is narrower than its parent, give it a fixed width and Auto left and right margins in [Spacing](spacing.md).
{% endhint %}

Specialised defaults include:

* **Image and Video** — Width `100%`, Height Auto.
* **SVG** — Width theme spacing 20, Height Auto.

### Min & Max Settings

**Enable** is off by default. Enabling it reveals:

* **Width → Min** — Defaults to 0.
* **Width → Max** — Defaults to Auto.
* **Height → Min** — Defaults to 0.
* **Height → Max** — Defaults to Auto.

Min values prevent a component shrinking below a limit. Max values prevent it growing beyond a limit. These settings are responsive.

{% hint style="info" %}
A maximum width improves readability for long text and prevents large screens stretching content too far. A minimum width should be used carefully because it can cause horizontal scrolling on small screens.
{% endhint %}

### Aspect Ratio

Image and Video share an Aspect Ratio control:

* **Auto** — Uses the source media’s natural ratio. This is the default.
* **Wide** — Uses 16:9.
* **Tall** — Uses 4:5.
* **Custom** — Reveals a ratio field, which defaults to `7/5`.

For a fixed ratio, **Object Fit** offers Fill, Contain, Cover, None, and Scale Down, defaulting to Cover.

**Position** sets the focal point inside the frame and defaults to Centre.

### Using Custom CSS Values

Switch a supported size control to manual mode to enter a valid CSS value. Common examples:

* `250px` — A fixed pixel size.
* `20rem` — A size relative to the root text size.
* `75%` — A percentage of the containing block.
* `100vw` — The full viewport width.
* `80vh` — 80% of the viewport height.
* `calc(100vw - 20px)` — The viewport width minus 20 pixels.
* `clamp(18rem, 50vw, 48rem)` — A responsive size with minimum and maximum limits.

See [CSS math functions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions/Using_CSS_math_functions) for `calc()`, `min()`, `max()`, and `clamp()`.

## Sizing UI in Elements

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-28 at 11 .51.11@2x.png" alt="Sizing controls for width, height, and minimum and maximum values"><figcaption><p>Sizing values can use Theme Spacing or custom CSS values.</p></figcaption></figure>
