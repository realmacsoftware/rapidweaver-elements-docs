---
description: Add Margin and Padding to Components.
---

# Spacing

The Spacing controls allow you to add Margin and Padding to an object. By default this control is disabled, this is to ensure the pading and margin classes are not applied to the object.

To set Padding and Margin you need to switch the "Enable" toggle to on.&#x20;

The "Mask & Paintbrush" icon will toggle the control between selecting from a Theme Preset and setting an arbitrary value. To change the arbitrary value by 5px increments, click and drag the mouse up and down. To change the value by increments of 1px hold down the `shift` key while dragging.

To link the opposite value, click the dashed line so the highlight is set to blue. This can be done independently for vertical and horizontal values.

{% embed url="https://youtu.be/8xS_OMqpw4U" %}

### Margin

The Margin property controls the space around an element, outside of its border. It creates space between the element and its neighboring elements.

Margins can be set for all four sides of an element—top, right, bottom, and left—or individually for each side.

{% hint style="info" %}
When you set a margin-right on a component, it creates space to the right of it. However, if there’s nothing positioned immediately to the right — like another component or a container edge — you might not see any visible change. This is a common CSS quirk that can feel a bit confusing at first, especially when you’re expecting the element itself to shift.
{% endhint %}

#### Auto margins and self-alignment

Setting a horizontal margin to **Auto** makes the element absorb the available free space on that side, which is how a component positions _itself_ within its parent:

* **Left Auto + Right Auto** — centres the element.
* **Left 0 + Right Auto** — pushes the element to the left.
* **Left Auto + Right 0** — pushes the element to the right.

Some components ship with Auto horizontal margins **enabled by default** so they align sensibly on their own. The **Button** component is the main example: its default margin is Top `0`, Right `Auto`, Bottom `0`, Left `Auto`, so a standalone button centres itself.

{% hint style="warning" %}
**Auto margins fight with Flex and Grid layouts.** When a component sits inside a [Flex](../flex.md) or [Grid](../grid.md) container, the parent already controls alignment and spacing (via its Justify, Align, and Gap settings). A child's Auto horizontal margins override that logic — each child absorbs the free space and the parent's centring/gap is ignored, producing uneven spacing.

If you place **Buttons** (or any component with default Auto margins) inside a Flex row or Grid, set all four margins to `0` so the parent controls the layout. Keep the Auto margins only when you want a single child to align itself (for example, one button pushed to the right with Left Auto + Right 0).
{% endhint %}

### Padding

The Padding property controls the space inside an element, between its content and the element’s border. Unlike margin, which affects the space outside an element, padding pushes the content inward, creating internal spacing within the element itself.

Padding can be set for all four sides of an element—top, right, bottom, and left—or individually for each side.

## Spacing UI in Elements

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-16 at 3 .05.02@2x.png" alt=""><figcaption><p>RapidWeaver Elements Component Spacing (October 2024)</p></figcaption></figure>
