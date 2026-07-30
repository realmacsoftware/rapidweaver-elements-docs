---
description: Let visitors choose one option from a group
---

# Radio

Radio creates a set of mutually exclusive choices. Selecting one option automatically clears the other option in the same group.

### How to Use Radio

You’ll find Radio under **Forms** in the Components list.

1. Place Radio inside a [Form](README.md).
2. Enter a shared Name for the group.
3. Add items to the Options collection.
4. Give every option a visible Label and submitted Value.
5. Enable Required when the visitor must make a choice.
6. Style checked, unchecked, label, and focus states.

### Component Settings

#### Settings

**Required** is off by default.

**Name** is blank by default. Every option uses this Name so the browser treats them as one group.

**Alignment** arranges options Horizontally or Vertically and defaults to Vertical.

#### Radio

Use **State** to edit Unchecked and Checked appearance. It defaults to Unchecked.

* **Unchecked** — Border Surface 900; Background Surface 50.
* **Checked** — Border Brand 500; Background Brand 500.

Border Width and Border Radius use Theme Studio controls.

#### Options

The **Options** collection adds, removes, and reorders choices. Each item contains:

* **Label** — Text shown to the visitor. Blank by default.
* **Value** — Value included in the submission. Blank by default.

#### Label

Label colours default to Surface 50 when Unchecked and Brand 500 when Checked.

**Font** defaults to Body and **Size** to Base.

#### Outline

**Type** defaults to None and can be Static or Focus. Focus provides Unfocused and Focused states.

Outline defaults are Solid style, Surface 500 colour, 100% opacity, width 1, and offset 0.

#### Sizing and Spacing

Radio **Size** defaults to theme spacing 4.

Option **Gap** defaults to theme spacing 4.

### Accessibility

Use a clear question or group description before the options and concise labels for each choice. Keep a visible keyboard-focus outline.

### Related Components

* [Checkbox](checkbox.md) — Allows several independent choices.
* [Select](select.md) — Presents one choice in a compact drop-down.
* [Form](README.md) — Configures delivery and validation.

{% include "../../../.gitbook/includes/common-controls.md" %}
