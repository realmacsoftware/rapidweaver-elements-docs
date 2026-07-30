---
description: Control component positioning, stacking, visibility, overflow, and isolation
---

# Layout

Layout controls how a component participates in the page layout. Use them to change positioning, offsets, stacking order, visibility, overflow, and stacking-context isolation.

### Position

**Position** defaults to None.

| Option | Behaviour |
| --- | --- |
| None | Adds no positioning rule. |
| Static | Keeps the component in normal document flow and ignores offsets. |
| Relative | Keeps its original space while allowing offsets and positioned descendants. |
| Absolute | Removes it from normal flow and positions it against the nearest positioned ancestor. |
| Fixed | Removes it from normal flow and positions it against the viewport. |
| Sticky | Behaves normally until it reaches an offset, then remains pinned within its scrolling ancestor. |

See [Tailwind CSS Position](https://tailwindcss.com/docs/position) for the equivalent CSS behaviour.

{% hint style="info" %}
Sticky positioning needs at least one non-Auto offset, usually **Top**. It can also be prevented by an ancestor’s overflow or insufficient scrollable height.
{% endhint %}

### Z-Index

**Z-Index** controls stacking order and is not responsive.

* **None** — Adds no z-index value. This is the default.
* **Auto** — Lets the browser determine the stack order.
* **Custom** — Reveals a number field, which defaults to 0 and accepts positive or negative values.

See [Tailwind CSS Z-Index](https://tailwindcss.com/docs/z-index) for the equivalent CSS behaviour.

{% embed url="https://youtu.be/tW5AMT6l6CY" %}

### Top, Right, Bottom, and Left

**Type** defaults to None.

* **None** — Adds no offsets.
* **Uniform** — Reveals one **Inset** value for all four sides. It defaults to 0.
* **Individual** — Reveals separate **Top**, **Right**, **Bottom**, and **Left** values. Each defaults to 0.

Offsets support responsive Theme Spacing or custom CSS values. They affect Relative, Absolute, Fixed, and Sticky positioning; Static ignores them.

See [Tailwind CSS Top, Right, Bottom, and Left](https://tailwindcss.com/docs/top-right-bottom-left).

{% embed url="https://youtu.be/2WZ0zacUgTI" %}

### Display

**Hidden** is off by default. Enable it at a breakpoint to remove the component from the rendered layout at that breakpoint and above until another responsive override changes it.

**Visibility** defaults to Auto.

* **Auto** — Adds no visibility rule.
* **Visible** — Shows the component.
* **Invisible** — Hides the component while preserving its layout space.

See [Tailwind CSS Visibility](https://tailwindcss.com/docs/visibility).

{% hint style="warning" %}
Hidden and Invisible are different: Hidden removes the component from layout; Invisible leaves an empty space where it would have appeared.
{% endhint %}

{% embed url="https://youtu.be/Lt9ZGrEG21M" %}

### Overflow

**Overflow** defaults to None.

* **None** — Adds no overflow rule.
* **Visible** — Allows content to extend beyond the component.
* **Hidden** — Clips overflowing content without scrollbars.
* **Scroll** — Always provides scrolling for overflowing content.
* **Auto** — Adds scrollbars only when content overflows.

See [Tailwind CSS Overflow](https://tailwindcss.com/docs/overflow).

{% embed url="https://youtu.be/rOHL-KScsqc" %}

### Isolation

**Isolation** defaults to None.

* **None** — Adds no isolation rule.
* **Isolate** — Creates a new stacking context so child z-index values remain within the component.
* **Auto** — Lets the browser decide whether a stacking context is needed.

See [Tailwind CSS Isolation](https://tailwindcss.com/docs/isolation).

### Flex and Grid Items

Some components also provide **Flexbox and Grid** item controls. These settings apply only when the component is inside the matching parent:

* **Grid Item** controls column, row, span, and placement.
* **Flex Item** controls order, growth, shrink, basis, and self-alignment.

Use the parent [Flex](../flex.md) or [Grid](../grid.md) controls for the overall layout, then use item controls only for exceptions.

## Layout UI in Elements

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-19 at 8 .02.46@2x.png" alt="Layout controls for position, z-index, offsets, visibility, overflow, and isolation"><figcaption><p>The appearance may have changed since this screenshot, but the underlying controls remain the same.</p></figcaption></figure>
