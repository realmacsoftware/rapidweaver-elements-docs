---
description: Let visitors filter content with selectable tag buttons
---

# Filter Tags

The Filter Tags component creates a set of buttons that visitors can use to show content matching one or more tags. It works with tags assigned to filter-enabled components such as Container, Grid, Flex, and Accordion.

### How to Use Filter Tags

You’ll find Filter Tags under **Interactive** in the Components list.

1. Add tags to each compatible component you want to filter.
2. Enable filtering on those components.
3. Place **Filter Tags** in the same parent, or use a matching custom Group ID.
4. Choose single or multiple selection and configure the matching behaviour.
5. Style the tag layout and button states.

### Component Settings

#### Settings

**Group**

* **Parent** — Controls filterable items inside the same parent. This is the default.
* **Custom** — Controls items that share the same Group ID.

**Group ID** appears for Custom grouping. Replace the default `unique-group-id` with the same unique value on the Filter Tags component and its target items.

**Mode**

* **Multiple** — Visitors can select more than one tag. This is the default.
* **Single** — Selecting a tag clears the previous selection.

**Match** is available in Multiple mode:

* **Any** — Shows an item when it matches at least one selected tag. This is the default.
* **All** — Shows an item only when it matches every selected tag.

#### Tags Layout

**Alignment** places the tag buttons at the Start, Center, or End. The default is Start.

**Gap** controls spacing between buttons and defaults to theme spacing 4.

#### Font and Text Styles

Set button alignment, font, size, weight, letter spacing, line height, case, italic, underline, text shadow, colour, and opacity. Use the state selector to style Normal and Hover text independently.

### Accessibility

Use clear tag names and maintain strong contrast for selected, unselected, hover, and focus states. Do not communicate selection with colour alone.

### Troubleshooting

#### Tags do not affect the expected items

Check that the target components have filtering enabled. For Custom grouping, all items and the Filter Tags component must use exactly the same Group ID.

### Related Components

* [Filter](filter.md) — Filters the same tagged content through a text search field.
* [Container](container.md) — A common wrapper for filterable cards and sections.

{% include "../../.gitbook/includes/common-controls.md" %}
