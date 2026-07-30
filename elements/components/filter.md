---
description: Let visitors search and filter tagged content by text
---

# Filter

The Filter component provides a search field that shows and hides filter-enabled components as the visitor types. It works with tags assigned to compatible components such as Container, Grid, Flex, and Accordion.

### How to Use Filter

You’ll find Filter under **Interactive** in the Components list.

1. Add the content components you want visitors to filter.
2. Add tags to each compatible component and enable its **Filter** controls.
3. Place a **Filter** component in the same parent, or give both the filter and content the same custom Group ID.
4. Edit the placeholder and style the input.
5. Preview the page and search for one of your tags.

### Component Settings

#### Settings

**Group** determines which items the search field controls:

* **Parent** — Filters compatible items inside the same parent. This is the default.
* **Custom** — Filters items that use the same custom Group ID.

**Group ID** appears when Custom is selected. The default value is `unique-group-id`; replace it with a value unique to that filter group.

#### Font and Text Styles

Set the input text colour, opacity, font, size, weight, letter spacing, line height, case, italic, and alignment. Normal and focus states can be styled independently where shown.

#### Placeholder

**Text** sets the empty-field prompt and defaults to “Filter…”.

**Color** sets the placeholder colour and defaults to Text 400.

#### Outline

Outline controls style the focus outline shown around the search field. Keep a visible focus indicator for keyboard users.

### Accessibility

Use a descriptive placeholder or nearby label so visitors understand what can be searched. Do not remove the keyboard focus outline unless you replace it with an equally clear focus style.

### Troubleshooting

#### Typing does not filter anything

Confirm that each target component has filtering enabled and contains matching tags. When using Custom grouping, the Filter and every target must use exactly the same Group ID.

### Related Components

* [Filter Tags](filter-tags.md) — Provides selectable tag buttons instead of a text search field.
* [Container](container.md) — A common wrapper for filterable content.

{% include "../../.gitbook/includes/common-controls.md" %}
