---
description: Write and render structured content using Markdown syntax
---

# Markdown

The Markdown component renders standard Markdown inside an Elements layout. It is useful for documentation, articles, technical content, and text written outside Elements.

Markdown content inherits a Theme Studio Typography style, keeping headings, paragraphs, lists, links, and code visually consistent.

### How to Use Markdown

You’ll find Markdown under **Content** in the Components list.

1. Drag **Markdown** onto the page.
2. Right-click the component and choose **Edit Markdown**.
3. Enter or paste Markdown in the editor.
4. Choose a Typography Style and semantic Tag in the Inspector.
5. Preview links, images, lists, and code on the page.

The content renders live as you type. You can also drag an image from Resources into the Markdown editor to insert its correct path.

{% embed url="https://youtu.be/ZkmYC_rAN4o" %}

### Supported Markdown Syntax

**Headings**

```markdown
# Heading 1
## Heading 2
### Heading 3
```

**Emphasis**

```markdown
*Italic text*
**Bold text**
***Bold and italic***
```

**Lists**

```markdown
- Unordered item
- Another item

1. First item
2. Second item
```

**Links and images**

```markdown
[Visit Realmac Software](https://realmacsoftware.com)
![Alternative text](https://example.com/photos/image-name.jpg)
```

**Quotes and code**

```markdown
> This is a blockquote.

`inline code`
```

Paragraphs are separated by a blank line. The component supports standard [Markdown syntax](https://daringfireball.net/projects/markdown/syntax).

### Component Settings

#### General

**Style** chooses a Theme Studio Typography style and defaults to Article. It styles all nested Markdown elements.

**Tag** sets the semantic wrapper and defaults to Article. Options are Article, Section, Aside, Main Content, Header, Footer, Div, and Span.

The tag changes document meaning rather than visual styling. Use Main Content only once per page.

### Notes and Limitations

* Markdown renders as static content.
* Elements components cannot be embedded inside Markdown.
* Visual styling is controlled at block level through Theme Studio.
* Use separate Elements components when you need fine-grained layout or interaction.

### Accessibility

Use one clear page heading, keep heading levels in order, describe images with useful alternative text, and write link text that makes sense out of context.

### Related Components

* [Typography](typography.md) — Styles long-form content as a structured block.
* [Text](text.md) — Gives detailed control over individual headings and short text.
* [Image](image.md) — Provides responsive image, alt text, and lightbox controls.

{% include "../../.gitbook/includes/common-controls.md" %}
