---
description: Add Margin and Padding to Components.
---

# Spacing

The Spacing controls allow you to add Margin and Padding to an object. By default this control is disabled, this is to ensure the pading and margin classes are not applied to the object.

To set Padding and Margin you need to switch the "Enable" toggle to on.

Padding creates space **inside** the element. Margin creates space **outside** the element.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-16 at 3 .05.02@2x.png" alt=""><figcaption><p>RapidWeaver Elements Component Spacing (October 2024)</p></figcaption></figure>

The "Mask & Paintbrush" icon will toggle the control between selecting from a Theme Preset and setting an arbitrary/manual value. To change the arbitrary value by 5px increments, click and drag the mouse up and down. To change the value by increments of 1px hold down the `shift` key while dragging.

To link the opposite value, click the dashed line so the highlight is set to blue. This can be done independently for vertical and horizontal values.

{% embed url="https://youtu.be/8xS_OMqpw4U" %}

### Margin

The Margin property controls the space around an element, outside of its border. It creates space between the element and its neighboring elements. Use them to separate a section, card, image, button, or text block from the content around it.

Margins can be set for all four sides of an element—top, right, bottom, and left—or individually for each side.

Enable **Spacing → Margin & Padding**, then set a value for each side of the margin diagram:

* **Top** adds space above the element.
* **Right** adds space to its right.
* **Bottom** adds space below it.
* **Left** adds space to its left.

The left and right Margin can be linked together by clicking the dotted line between them, the top and bottom Margin can be linked together by clicking the dotted line between them also.

The Mask icon switches between Theme Preset values, and full manual control. Manual control is useful if you want to set negative values.

Choose **auto** when the browser should calculate the margin for you. The most common use is horizontal centring:

* Set the **left** and **right** margins to `auto`.
* Give the element a width or maximum width.

`auto` is generally most useful on the left and right sides. For top and bottom margins, use a numeric spacing value unless you have a specific layout reason to use automatic margins.

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

Enable **Spacing → Margin & Padding**, then choose a padding value for each side of the diagram:

* **Top** adds space above the content.
* **Right** adds space to the right of the content.
* **Bottom** adds space below the content.
* **Left** adds space to the left of the content.

You can set each side independently, which is helpful for layouts such as a banner with more space above and below its text than at the sides.

#### Padding and backgrounds

Padding is particularly important when an element has a background colour, border, or rounded corners. It expands the area inside those visual boundaries, so the content does not sit against the edge.

For example, a card may use:

* `6` padding on every side for comfortable internal spacing.
* A larger top and bottom value for a promotional panel or callout.
* Smaller horizontal padding on a compact button.
