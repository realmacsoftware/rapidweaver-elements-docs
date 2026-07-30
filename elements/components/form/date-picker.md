---
description: Collect a date and optional time
---

# Date Picker

Date Picker provides a formatted date field with a calendar interface. It can also collect a time.

### How to Use Date Picker

You’ll find Date Picker under **Forms** in the Components list.

1. Place Date Picker inside a [Form](README.md).
2. Enter a unique Name.
3. Choose the Date Format.
4. Enable Time if required.
5. Add a [Label](label.md) whose For value matches the Name.
6. Publish and test keyboard entry and calendar selection.

### Component Settings

#### Settings

**Name** is blank by default. If left blank, Elements creates a generated name.

**Required** is off by default.

**Date Format** is not responsive and defaults to `Y-m-d`, displayed as `2026-02-26`. Other formats are:

* `m/d/Y` — `02/26/2026`
* `d/m/Y` — `26/02/2026`
* `F j, Y` — `February 26, 2026`

**Enable Time** is off by default. Enabling it appends a 24-hour hours-and-minutes value to the selected date.

**Placeholder** defaults to “Select a date…”.

Placeholder **Color** defaults to Text 400.

#### Input

Input **Color** defaults to Text 50.

**Font** defaults to Body and **Size** to Base.

#### Outline

**Type** defaults to None and can be Static or Focus. Focus provides Unfocused and Focused states.

Outline defaults are Solid style, Surface 500 colour, 100% opacity, width 1, and offset 0.

The field uses the shared Input sizing and spacing defaults: 100% width, Auto height, zero margin, and padding 2 vertically and 3.5 horizontally.

### Accessibility

Add a Label, preserve a visible focus state, and choose a date format familiar to the intended audience. Visitors can type directly into the field as well as use the calendar.

### Related Components

* [Input](input.md) — Collects text and other single-value fields.
* [Label](label.md) — Associates visible text with the Date Picker.
* [Form](README.md) — Configures delivery and validation.

{% include "../../../.gitbook/includes/common-controls.md" %}
