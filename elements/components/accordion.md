---
description: Organise content into expandable and collapsible sections
---

# Accordion

The Accordion component organises content into sections that visitors can open and close. It is useful for FAQs, service details, feature explanations, and other pages where displaying everything at once would create unnecessary scrolling.

Each Accordion has separate Title and Content drop zones, so both areas can contain Text, Images, SVGs, or other suitable components.

{% embed url="https://youtu.be/w1pfxSfHN5o" %}

### How to Use Accordion

You’ll find Accordion under **Interactive** in the Components list.

1. Drag **Accordion** onto the page.
2. Add components to its Title and Content drop zones.
3. Choose whether it starts Open or Closed.
4. Use Grouping when only one Accordion in a set should remain open.
5. Style the Summary and optional SVG icon for open and closed states.

<figure><img src="../../.gitbook/assets/CleanShot 2025-04-27 at 11 .24.50@2x.png" alt="The Accordion component highlighted in the Interactive section of the Components list"><figcaption><p>The Accordion component is in the Interactive category.</p></figcaption></figure>

### Component Settings

#### Settings

**Show Content in Edit** is enabled by default. Disable it to preview the collapsed structure while editing.

**Default State** chooses Open or Closed and defaults to Closed.

#### Tags

Add one or more tag titles when the Accordion should be controlled by Filter or Filter Tags.

#### Filter

Enable filtering to make the Accordion a filterable item. Use Parent grouping or a Custom Group ID, then choose the Dim, Zoom Out, or Slide transition.

#### Grouping

**Group**

* **None** — The Accordion opens independently.
* **Parent** — Groups Accordions inside the same parent. This is the default.
* **Custom** — Groups Accordions that share a Group ID.

**Group ID** appears for Custom. Replace the default `unique-group-id` with the same value on every Accordion in the group.

Grouping ensures that opening one Accordion closes the others in the same group.

#### Summary

**State** switches the Inspector between Open and Closed styling. It defaults to Closed.

Each state has its own **Background** colour. Both default to None.

**Padding** applies to the clickable summary area and defaults to theme spacing 2 vertically and 3.5 horizontally.

#### Icon

**Show Icon** is enabled by default.

* **SVG** — Selects the icon resource.
* **Alignment** — Places the icon first or last. Last is the default.
* **Size** — Accepts any valid CSS size and defaults to `24px`.
* **State** — Switches between Open and Closed icon styling.
* **Rotation** — Defaults to 90° for Open and 180° for Closed.
* **Color** — Sets the SVG colour for each state and defaults to Surface 900.

### Accessibility

Use concise, descriptive titles that explain the hidden content. Do not place essential information only in a closed section without making the title clear.

### Tips and Best Practices

* **Group related items:** Parent grouping is the simplest way to create a traditional one-at-a-time accordion.
* **Keep titles short:** Visitors should be able to scan the complete set quickly.
* **Use a familiar icon:** Chevrons and plus/minus symbols clearly communicate expansion.

### Related Components

* [Tabs](tabs.md) — Switches between parallel content sections.
* [Dropdown](dropdown.md) — Reveals a compact panel from a trigger.
* [Filter Tags](filter-tags.md) — Can show and hide tagged Accordions.

{% include "../../.gitbook/includes/common-controls (1).md" %}
