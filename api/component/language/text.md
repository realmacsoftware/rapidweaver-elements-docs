---
description: Add editable plain text areas to your components
---

# @text

The `@text` directive creates an editable plain text area within your component. This is ideal for headings, labels, button text, and any single-line or simple multi-line text content.

## Syntax

```html
@text("identifier")
```

Or with additional parameters:

```html
@text(name: "identifier", title: "Display Title", default: "Default text")
```

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `name` | Yes | A unique identifier for the text area within the component |
| `title` | No | The label displayed in the editor interface |
| `default` | No | Default text to display when no content has been entered |

## Examples

### Basic Text Area

Create a simple editable text area:

```html
<h1>@text("heading")</h1>
```

### With Default Value

Provide default text that users can modify:

```html
<h2>@text("heading", default: "Hello World!")</h2>
```

### With Title for Editor

Add a descriptive title that appears in the editor interface:

```html
@text(name: "content", title: "Text")
```

### Button with Conditional Text

Combine `@text` with conditionals to show text only when enabled:

```html
@if(showText)
    @text("text", title: "Button Text", default: "Click Me")
@endif
```

### Form Labels

```html
<label for="email">
    @text("emailLabel", default: "Email Address")
</label>
<input type="email" id="email" />
```

### Navigation Title

```html
<nav>
    <a href="/" class="brand">
        @text("siteTitle", title: "Site Title", default: "My Website")
    </a>
</nav>
```

### Using @text Inside an @each Loop

You can use the `@text` directive inside an `@each` loop to create unique editable text areas for each iteration. The loop index is automatically appended to the identifier, ensuring each text area remains distinct:

```html
@each(item in items)
    <div class="card">
        <h3>@text("cardTitle", default: "Card Title")</h3>
    </div>
@endeach
```

In this example, if the loop iterates three times, it will create three unique text areas, each independently editable.

## Best Practices

1. **Use descriptive identifiers** - Choose names that clearly indicate the text's purpose (e.g., `"heading"`, `"buttonLabel"`, `"siteTitle"`).

2. **Provide helpful defaults** - Default text helps users understand the expected content and provides a starting point.

3. **Add titles for clarity** - The `title` parameter helps users identify the text area in the editor, especially when there are multiple text areas.

4. **Use for simple content** - For rich formatting needs, consider [@richtext](richtext.md) or [@markdown](markdown.md) instead.

## Related

- [@richtext](richtext.md) - For styled text with Typography support
- [@markdown](markdown.md) - For Markdown-formatted content
