---
description: Apply a Theme Studio typography style to long-form content
---

# Typography

The Typography component is designed for long-form, structured content containing headings, paragraphs, lists, links, quotes, and other text elements. It applies one Theme Studio typography style across the entire content block.

Use Typography when you want consistent editorial styling without configuring each text element independently.

### How to Use Typography

You’ll find Typography under **Content** in the Components list.

1. Drag **Typography** onto the page.
2. Add or edit the long-form content inside the component.
3. Choose a Theme Studio typography **Style**.
4. Select the semantic HTML tag that best describes the block.
5. Adjust shared sizing, spacing, background, borders, and effects if required.

### Component Settings

#### General

**Style** selects a Typography style from Theme Studio and defaults to Article. The style controls the appearance of headings, paragraphs, lists, links, and other nested text.

**Tag** sets the semantic wrapper and is not responsive. Options are Article, Section, Aside, Main Content, Header, Footer, Div, and Span. Article is the default.

Choose the tag for meaning rather than appearance:

* **Article** — Self-contained editorial content.
* **Section** — A thematic section of a page.
* **Aside** — Supporting or secondary content.
* **Main Content** — The page’s primary content; use only once per page.
* **Header** or **Footer** — Introductory or closing content for a page or section.
* **Div** or **Span** — Neutral wrappers when no semantic option applies.

### Tips and Best Practices

#### Manually styling links in lists

In **Typography → Advanced**, add these classes:

```css
[&_a]:!font-body
[&_a]:text-brand-500
[&_a]:underline-offset-2
[&_a:hover]:underline
```

This styles links inside lists used within the Typography component.

### Accessibility

Keep heading levels in a logical order and choose a semantic wrapper that matches the content. Link text should describe its destination without relying on surrounding text.

### Related Components

* [Markdown](markdown.md) — Writes and renders long-form content using Markdown syntax.
* [Text](text.md) — Gives precise styling control over individual headings and short text blocks.

{% include "../../.gitbook/includes/common-controls (1).md" %}
