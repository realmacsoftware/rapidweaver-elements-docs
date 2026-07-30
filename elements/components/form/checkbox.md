---
description: Let visitors choose zero, one, or several options
---

# Checkbox

Checkbox creates a group of independently selectable options. Use it for preferences, opt-ins, feature choices, or required acknowledgements.

### How to Use Checkbox

You’ll find Checkbox under **Forms** in the Components list.

1. Place Checkbox inside a [Form](README.md).
2. Enter a shared Name for the group.
3. Add items to the Options collection.
4. Give every option a visible Label and submitted Value.
5. Enable Required only when every displayed option must be selected.
6. Style checked, unchecked, label, and focus states.

### Component Settings

#### Settings

**Required** is off by default. When enabled, each rendered Checkbox option is marked as required, so use it when every listed acknowledgement must be selected.

**Name** is blank by default. Checkbox submits the selected values as a group using this name.

**Alignment** arranges options Horizontally or Vertically and defaults to Vertical.

#### Checkbox

Use **State** to edit Unchecked and Checked appearance. It defaults to Unchecked.

* **Unchecked** — Border Surface 50; Background Surface 50.
* **Checked** — Border Brand 500; Background Brand 500.

Border Width and Border Radius use Theme Studio controls.

#### Options

The **Options** collection adds, removes, and reorders choices. Each item contains:

* **Label** — Text shown to the visitor. Blank by default.
* **Value** — Value included in the submission. Blank by default.

Use a stable machine-friendly Value such as `newsletter` rather than repeating a long sentence.

#### Label

Label colours default to Surface 50 when Unchecked and Brand 500 when Checked.

**Font** defaults to Body and **Size** to Base.

#### Outline

**Type** defaults to None and can be Static or Focus. Focus reveals Unfocused and Focused states.

Outline defaults are Solid style, Surface 500 colour, 100% opacity, width 1, and offset 0.

#### Sizing and Spacing

Checkbox **Size** defaults to theme spacing 4.

Option **Gap** defaults to theme spacing 4.

### Accessibility

Use labels that make sense when read independently. Keep a visible keyboard-focus outline and place required legal consent in clear text rather than relying on colour or position.

### Related Components

* [Radio](radio.md) — Allows exactly one choice from a group.
* [Label](label.md) — Labels individual fields.
* [Form](README.md) — Configures delivery and validation.

{% include "../../../.gitbook/includes/common-controls.md" %}
