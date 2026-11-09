---
description: Add editable rich text areas with Typography styling support
---

# @richtext

The `@richtext` directive creates an editable text area that supports the Typography feature for rich text styling. This allows users to apply theme-based text styles, formatting, and typography settings to their content.

## Syntax

```html
@richtext("identifier", title: "Display Title")
```

Or with a default value:

```html
@richtext("identifier", title: "Display Title", default: "Default content")
```

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `name` | Yes | A unique identifier for the rich text area within the component |
| `title` | No | The label displayed in the editor interface |
| `default` | No | Default content to display when no content has been entered |

## Examples

### Basic Rich Text Area

```html
@richtext("content", title: "Typography")
```

### With Default Content

```html
@richtext("heading", default: "Hello World!")
```

### Article Content

```html
<article>
    <header>
        @richtext("title", title: "Article Title", default: "Untitled Article")
    </header>
    <div class="content">
        @richtext("body", title: "Article Body")
    </div>
</article>
```

### Hero Section

```html
<section class="hero">
    <div class="hero-content">
        @richtext("heroTitle", title: "Hero Title", default: "Welcome")
        @richtext("heroSubtitle", title: "Hero Subtitle", default: "Discover something amazing")
    </div>
</section>
```

### Using @richtext Inside an @each Loop

You can use the `@richtext` directive inside an `@each` loop to create unique editable rich text areas for each iteration. The loop index is automatically appended to the identifier, ensuring each rich text area remains distinct:

```html
@each(item in items)
    <div class="card">
        <h3>@richtext("cardTitle", default: "Card Title")</h3>
    </div>
@endeach
```

In this example, if the loop iterates three times, it will create three unique rich text areas, each independently editable with full Typography support.

## Typography Integration

The `@richtext` directive integrates with the Elements Typography system, allowing users to:

- Apply predefined text styles from the theme
- Adjust font family, size, weight, and line height
- Set text colors from the theme palette
- Apply letter spacing and text transforms
- Use responsive typography settings

When users click on a rich text area in the editor, the Typography panel becomes available, providing access to all text styling options defined in the active theme.

## When to Use @richtext

Use `@richtext` when:

- Content needs theme-based typography styling
- Users should be able to apply text styles from the Typography panel
- The text is a prominent element like headings or featured content

For simpler use cases:

- Use [@text](text.md) for plain text without styling (labels, simple headings)
- Use [@markdown](markdown.md) for structured content with Markdown formatting

## Related

- [@text](text.md) - For simple plain text editing
- [@markdown](markdown.md) - For Markdown-formatted content
- [Theme Typography](../properties.json/ui-controls/theme-typography.md) - Typography UI control documentation
