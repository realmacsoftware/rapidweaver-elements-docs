---
description: Collect text, email, numbers, passwords, telephone numbers, URLs, or multi-line content
---

# Input

Input creates a single form field. Its Type selects the appropriate browser input, validation, keyboard, and autofill behaviour.

### How to Use Input

You’ll find Input under **Forms** in the Components list.

1. Place Input inside a [Form](README.md).
2. Choose the correct Type.
3. Enter a short, unique Name.
4. Add a [Label](label.md) whose For value exactly matches the Name.
5. Set Required and Placeholder as needed.
6. Style the text, border, background, and focus outline.

### Component Settings

#### Settings

**Type** is not responsive and defaults to Text:

* Text
* Textarea
* Email
* Number
* Password
* Search
* Telephone
* URL

Textarea reveals **Rows**, which defaults to 3.

**Name** is blank by default. If left blank, Elements generates a name. Use letters, numbers, hyphens, or underscores and do not reuse a Name within the Form.

**Required** is off by default.

**Placeholder** defaults to “Placeholder”.

Placeholder **Color** defaults to Text 400.

{% hint style="info" %}
Name an Email input exactly `email` when the submitted address should become the email’s Reply-To address.
{% endhint %}

#### Input

Input text **Color** defaults to Text 50.

**Font** defaults to Body and **Size** to Base.

#### Outline

**Type** defaults to None:

* **None** — Adds no outline.
* **Static** — Uses one outline style.
* **Focus** — Provides Unfocused and Focused states.

Outline defaults are Solid style, Surface 500 colour, 100% opacity, width 1, and offset 0.

Keep a visible Focus state for keyboard users.

#### Shared Input Defaults

Input uses 100% Width and Auto Height.

Spacing is enabled with zero Margin and Padding 2 vertically and 3.5 horizontally.

The Border is Static by default with Solid style, Surface 900 colour, 100% opacity, Theme Default width, and no radius.

### Accessibility

Use the most specific Type, add a visible Label, and do not use Placeholder as the only label. Explain required formats or password rules before the field.

### Related Components

* [Label](label.md) — Connects descriptive text to the Input.
* [Date Picker](date-picker.md) — Adds a calendar interface.
* [Select](select.md) — Presents a fixed list of choices.

{% include "../../../.gitbook/includes/common-controls (1).md" %}
