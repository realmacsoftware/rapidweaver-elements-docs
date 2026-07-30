---
description: Create fixed, angled, coloured, gradient, image, or SVG backgrounds
---

# Background

The Background component places a visual background behind optional child content. It supports solid colours, gradients, resource or CMS images, SVG artwork, fixed positioning, and angled edges.

{% embed url="https://youtu.be/YlKQaLTm1hY" %}

{% hint style="info" %}
Use a [Container](container.md) when your main goal is grouping and laying out content. Use Background when you need fixed imagery or angled edges.
{% endhint %}

### How to Use Background

You’ll find Background under **Layout** in the Components list.

1. Drag **Background** onto the page.
2. Leave the drop zone enabled and add content, or disable it for a purely decorative background.
3. Choose Color, Image, Gradient, or SVG under **Background → Style**.
4. Enable Fixed or Angle if required.
5. Adjust sizing and spacing, then preview at every breakpoint.

<figure><img src="../../.gitbook/assets/CleanShot 2025-04-28 at 4 .23.29@2x.png" alt="The Background component highlighted in the Layout section of the Components list"><figcaption><p>The Background component is in the Layout category.</p></figcaption></figure>

### Component Settings

#### Dropzone

**Enabled** controls whether the component accepts child content. It is on by default.

#### Angle

**Enable** turns angled edges on and is off by default.

**Mode**

* **Vertical** — Adjusts the left and right positions of the top and bottom edges. This is the default.
* **Horizontal** — Adjusts the top and bottom positions of the left and right edges.

Vertical mode defaults to Top Left 100%, Top Right 80%, Bottom Left 0%, and Bottom Right 0%. Horizontal mode defaults to Left Top 100%, Left Bottom 100%, Right Top 60%, and Right Bottom 30%.

#### Background

**Fixed** keeps the background anchored while page content scrolls. It is off by default.

**Style**

* **Color** — Uses a theme colour and opacity. Brand 500 at 100% is the default.
* **Image** — Uses a project Resource or CMS field.
* **Gradient** — Creates a Linear, Radial, or Conic gradient.
* **SVG** — Positions and sizes an SVG resource behind the content.

**Image**

Choose Resource or CMS. CMS defaults to `{{item.image.src}}`. Position defaults to Centre, Size to Cover, Repeat to No Repeat, and Fetch Priority to Auto.

**Gradient**

Choose Linear, Radial, or Conic; Linear is the default. Set its direction, centre, or starting angle, then choose colour interpolation. From and To colours default to Brand 200 and Brand 500 at positions 0% and 100%. **Add Via** adds an optional middle stop at 50%, defaulting to Brand 400.

**SVG**

Select the resource, then set Color and Opacity. Width and Height each provide Fixed, Max, and Min controls. Position uses Top, Right, Bottom, and Left offsets, while Translate X and Y apply final adjustments.

### Accessibility

Decorative backgrounds should not contain essential text. Maintain sufficient contrast between the background and all foreground content, and avoid fixed imagery that makes scrolling uncomfortable.

### Tips and Best Practices

* **Use Fixed sparingly:** Large fixed images can be distracting and may behave differently on mobile browsers.
* **Keep text readable:** Use colour or overlay choices that preserve contrast over the entire image.
* **Use responsive angles:** Review angled edges at every breakpoint so they do not cover content.

### Related Components

* [Container](container.md) — Provides richer content layout and background video controls.
* [Divider](divider.md) — Adds a simple visual break between sections.

{% include "../../.gitbook/includes/common-controls (1).md" %}
