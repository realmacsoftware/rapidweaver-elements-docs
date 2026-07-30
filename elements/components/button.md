---
description: Create a styled action or navigation control
---

# Button

The Button component creates a prominent clickable control for navigation or actions such as opening a Modal. It supports editable text, optional content drop zones, responsive sizing, and separate normal and hover styles.

{% embed url="https://youtu.be/4zXtboiY8nY" %}

### How to Use Button

You’ll find Button under **Content** in the Components list.

1. Drag **Button** onto the page.
2. Edit its label directly on the page.
3. Set the destination in **Link → To**.
4. Configure text, background, border, and hover styles.
5. Optionally enable a Left or Right drop zone for an SVG, Image, or other small component.

### Component Settings

#### Link

**To** sets the destination. Choose a page, resource, website, email address, phone number, anchor, or other supported link type.

#### Font and Text Styles

**Show** displays the button label and is enabled by default.

Use **State** to style Normal and Hover text independently:

* **Color** and **Opacity** — Default to Surface 50 at 100%.
* **Text Shadow** — Defaults to None.

General controls include Align, Family, Size, Weight, Spacing, Line Height, Case, Italic, and Underline. Alignment defaults to Centre, font to Body, size to Base, weight to 400, spacing and line height to Normal, and other styles to off.

#### Dropzone

**Dropzone**

* **None** — Uses text only. This is the default.
* **Left** — Adds a drop zone before the label.
* **Right** — Adds a drop zone after the label.

**Spacing** appears when a drop zone is enabled and defaults to theme spacing 2.

#### Background

Choose None, Static, or Hover. Hover is the default and provides separate Start and End styles. Background Style can be Color, Image, or Gradient. Image controls include position, size, repeat, and fetch priority; Gradient controls include type, direction, interpolation, colour stops, opacity, and stop positions.

### Common Layout Structure for Buttons

Use a **Flex** component when you want to control a group of buttons:

1. Add a **Container**.
2. Add a **Flex** inside the Container.
3. Add two or more **Buttons** inside the Flex.

<figure><img src="../../.gitbook/assets/CleanShot 2026-07-15 at 11 .07.37@2x.png" alt="Two centre-aligned Button components inside a Flex component"><figcaption><p>Centre-aligned Buttons inside a Flex component.</p></figcaption></figure>

Set Flex Direction to Row, Justify to Centre, and Align Items to Centre.

{% hint style="info" %}
Buttons use Auto left and right margins by default. When a Flex or Grid should control alignment and gaps, set each Button’s margins to 0. Changing Button padding does not reset its margins.
{% endhint %}

### Accessibility

Use action-oriented labels that describe the result, such as “Download Guide” rather than “Click Here”. Keep visible hover and keyboard focus states, and do not place interactive components inside a linked Button.

### Related Components

* [Flex](flex.md) — Aligns and spaces groups of Buttons.
* [Modal](modal.md) — Can be opened from a Button.
* [SVG](svg.md) — Adds a custom icon through the Button drop zone.

{% include "../../.gitbook/includes/common-controls.md" %}
