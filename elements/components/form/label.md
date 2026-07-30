---
description: Associate visible descriptive text with a form field
---

# Label

Label creates a semantic HTML label for an Input, Date Picker, Select, or other named field. A correctly connected label helps visitors understand and activate the field.

### How to Use Label

You’ll find Label under **Forms** in the Components list.

1. Place Label inside a [Form](README.md), close to its field.
2. Edit the label text directly on the canvas.
3. Copy the field’s Name exactly.
4. Enter that value under Label → For.
5. Preview the published form and click the label to confirm that its field receives focus.

### Component Settings

#### Settings

**For** defaults to `inputName`.

Replace it with the exact **Name** of the related field. Values are case-sensitive:

```text
email
```

If the Input Name is `email` but Label For is `Email`, they are not connected.

#### Text Styles

**Color** defaults to Text 50.

**Align** is not responsive, offers Start, Centre, or End, and defaults to Start.

Shared text-style defaults include Body Font, Base Size, weight 400, Normal spacing and line height, no text shadow, no case conversion, and no decoration.

### Accessibility

Use a visible Label for every field. Keep it descriptive and concise; Placeholder text disappears during entry and is not a replacement for a label.

### Troubleshooting

#### Clicking the label does not focus the field

Make sure For and the field Name are identical, with no spaces added before or after either value.

### Related Components

* [Input](input.md) — Collects a typed value.
* [Date Picker](date-picker.md) — Collects a date and optional time.
* [Select](select.md) — Presents a list of choices.

{% include "../../../.gitbook/includes/common-controls (1).md" %}
