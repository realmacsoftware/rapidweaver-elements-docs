---
description: Add editable Markdown text areas to your components
---

# @markdown

The `@markdown` directive creates an editable Markdown text area within your component. Users can write content using Markdown syntax, which is automatically converted to HTML when the page is rendered.

## Syntax

```html
@markdown(name: "content", title: "Content")
```

Or using positional parameters:

```html
@markdown("content", title: "Content")
```

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `name` | Yes | A unique identifier for the Markdown area within the component |
| `title` | No | The label displayed in the editor interface |
| `default` | No | Default Markdown content to display when no content has been entered |

## Examples

### Basic Markdown Area

```html
@markdown(name: "content", title: "Content")
```

### With Default Content

Provide helpful default content that guides users on how to use the Markdown editor:

```html
@markdown("content", title: "Markdown", default: "## Markdown

Right-click on this text and choose *Edit Markdown* from the contextual menu to show the Markdown editor.

Learn more in the [Markdown docs](../../../elements/components/markdown.md).")
```

### Article Body

```html
<article class="prose">
    @markdown("body", title: "Article Content", default: "## Getting Started

Write your article content here using **Markdown** syntax.

- Lists are supported
- As are *emphasis* and **strong** text
- And [links](https://example.com)")
</article>
```

## Markdown Features

The Markdown editor supports standard Markdown syntax including:

- **Headings** (`#`, `##`, `###`, etc.)
- **Emphasis** (`*italic*`, `**bold**`)
- **Lists** (ordered and unordered)
- **Links** (`[text](url)`)
- **Images** (`![alt](src)`)
- **Code blocks** (fenced with triple backticks)
- **Blockquotes** (`>`)
- **Horizontal rules** (`---`)

## Editor Integration

Users can access the Markdown editor by right-clicking on the Markdown area in the Elements editor and selecting "Edit Markdown" from the contextual menu. This opens a dedicated Markdown editing interface.

## Related

- [@text](text.md) - For simple plain text editing
- [@richtext](richtext.md) - For styled text with Typography support