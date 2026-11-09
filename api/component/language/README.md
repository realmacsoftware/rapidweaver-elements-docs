---
description: Template syntax reference for RapidWeaver Elements components
icon: brackets-curly
---

# Elements Language

The Elements Language is a lightweight yet powerful templating system built into RapidWeaver Elements. It uses `{{…}}` syntax for property insertion and provides expressive directives like `@if`, `@each`, and `@include` for dynamic content generation. The language is designed to keep your templates clean, intuitive, and focused on HTML structure.

## Property Insertion

Use double curly braces to insert component properties, page data, or collection values directly into your markup:

```html
<h2>{{title}}</h2>
<p>{{description}}</p>
<a href="{{link.href}}">{{link.title}}</a>
```

Access nested properties using dot notation:

```html
<span>{{author.name}}</span>
<img src="{{image.resource.src}}" alt="{{image.alt}}" />
```

## Directives Reference

### Content Areas

| Directive   | Description                          | Documentation            |
| ----------- | ------------------------------------ | ------------------------ |
| `@dropzone` | Container for child elements         | [Dropzones](dropzone.md) |
| `@text`     | Editable plain text area             | [Text](text.md)          |
| `@richtext` | Editable styled text with Typography | [Rich Text](richtext.md) |
| `@markdown` | Editable Markdown text area          | [Markdown](markdown.md)  |

### Control Flow

| Directive                   | Description              | Documentation         |
| --------------------------- | ------------------------ | --------------------- |
| `@if` / `@elseif` / `@else` | Conditional rendering    | [Conditionals](if.md) |
| `@each`                     | Iterate over collections | [Looping](each.md)    |

### Code Organization

| Directive    | Description                     | Documentation                               |
| ------------ | ------------------------------- | ------------------------------------------- |
| `@include`   | Include external template file  | [Includes](include.md)                      |
| `@includeIf` | Conditional template include    | [Includes](include.md#conditional-includes) |
| `@template`  | Define inline reusable template | [Inline Templates](template.md)             |

### Page Integration

| Directive | Description                         | Documentation        |
| --------- | ----------------------------------- | -------------------- |
| `@portal` | Transport content to page locations | [Portals](portal.md) |
| `@anchor` | Create linkable anchor points       | [Anchors](anchor.md) |
| `@raw`    | Disable template processing         | [Raw Output](raw.md) |

## Quick Examples

### Editable Text Areas

```html
@text("heading", default: "Welcome")
```

```html
@richtext("content", title: "Body Content")
```

```html
@markdown("article", title: "Article", default: "Write your content here...")
```

### Dropzones for Child Elements

```html
@dropzone("content", title: "Container")
```

```html
@dropzone(name: "items", title: "Grid Items", horizontal: true)
```

### Conditional Rendering

```html
@if(showHeader)
    <header>{{headerText}}</header>
@endif
```

```html
@if(edit)
    <!-- Edit mode content -->
@elseif(preview)
    <!-- Preview mode content -->
@else
    <!-- Published content -->
@endif
```

{% hint style="warning" %}
A template `@if` accepts a **single** condition (optionally negated with `!`). Boolean operators (`&&`, `||`) and comparisons (`==`, `>`, etc.) are **not** allowed and cause a lexer error. See [Combining Conditions](if.md#combining-conditions) for the supported alternatives.
{% endhint %}

### Looping Over Collections

```html
@each(item in items)
    <li>{{item.title}}</li>
@endeach
```

```html
@each(page in pages)
    @if(page::isFirst)
        <li class="first">{{page.title}}</li>
    @else
        <li>{{page.title}}</li>
    @endif
@endeach
```

### Including Templates

```html
@include("button", label: "Click Me", style: "primary")
```

```html
@includeIf(wantsLightbox, template: "lightbox")
```

### Portals for Script Injection

```html
@portal(bodyEnd, id: "my-script", includeOnce: true)
    <script src="library.js"></script>
@endportal
```

### Inline Templates

```html
@template("card")
    <div class="card">
        <h3>{{title}}</h3>
        <p>{{description}}</p>
    </div>
@endtemplate

@each(item in cards)
    @include("card", title: item.title, description: item.desc)
@endeach
```

### Anchor Points

```html
<section id="@anchor("features")">
    <h2>Features</h2>
</section>
```

### Raw Output for CMS Integration

```html
@raw()
    <div>{{cms.field}}</div>
@endraw
```

## Best Practices

1. **Keep templates focused on HTML** - Use the [hooks file](../hooks.js/) for complex logic, string manipulation, and data processing.
2. **Use meaningful property names** - Choose descriptive names that indicate purpose: `showHeader`, `buttonLabel`, `heroImage`.
3. **Extract repeated patterns** - Use `@include` or `@template` for reusable markup.
4. **Leverage conditionals for modes** - Use `edit` and `preview` variables to show appropriate content in each mode.
5. **Organize portal content** - Use `includeOnce` and consistent `id` values to prevent duplicate script/style injection.
