---
description: Let visitors choose an option from a drop-down list
---

# Select

Select creates a native drop-down field populated from an Options collection. It is useful when visitors must choose one value from a defined list.

### How to Use Select

You’ll find Select under **Forms** in the Components list.

1. Place Select inside a [Form](README.md).
2. Enter a unique Name.
3. Set the Placeholder.
4. Add Label and Value pairs to the Options collection.
5. Optionally mark one item as Default.
6. Add a [Label](label.md) whose For value matches the Name.

### Component Settings

#### Settings

**Required** is off by default.

**Name** is blank by default. If left blank, Elements generates a name.

**Placeholder** defaults to “Select an option…”. It has an empty value and remains selected until a visitor chooses an option, unless a Default item is configured.

#### Select

Text **Color** defaults to Text 50.

**Font** defaults to Body and **Size** to Base. These settings also style the drop-down arrow.

#### Options

Each item in the **Options** collection contains:

* **Label** — Text shown to the visitor. Blank by default.
* **Value** — Value included in the submission. Blank by default.
* **Default** — Selects that option initially. Off by default.

Only the first item marked Default is selected.

#### Outline

**Type** defaults to None and can be Static or Focus. Focus provides Unfocused and Focused states.

Outline defaults are Solid style, Surface 500 colour, 100% opacity, width 1, and offset 0.

#### Shared Input Defaults

Select uses 100% Width and Auto Height.

Spacing is enabled with zero Margin and Padding 2 vertically and 3.5 horizontally.

Background supports a colour. The shared Border defaults to None.

### Accessibility

Add a visible Label and make every option understandable without surrounding context. When Select is Required, keep the empty Placeholder so the visitor must make an intentional choice.

### Related Components

* [Radio](radio.md) — Shows all choices at once.
* [Input](input.md) — Collects a free-form value.
* [Label](label.md) — Associates visible text with Select.

{% include "../../../.gitbook/includes/common-controls.md" %}
