---
icon: table-layout
---

# Templates

Template files in RapidWeaver Elements house all the HTML, CSS, JavaScript, and other assets your component needs to work seamlessly. All template files are dynamically processed by Elements, allowing for property replacements, conditional rendering, iterations, and more using the [Elements Language](../language/README.md). This enables you to build highly flexible and reusable components.

## Overview

The templates directory is the heart of your component's output. Files placed here are processed using the Elements templating language, which supports:

- **Property insertion** using `{{propertyName}}` syntax
- **Conditional rendering** with `@if`, `@elseif`, `@else`
- **Loops** using `@each` for collections
- **Content areas** with `@dropzone`, `@text`, `@richtext`, and `@markdown`
- **Template includes** with `@include` for reusable partials
- **Portal injection** using `@portal` to place content in specific page locations
- **Literal output** using `@raw` to stop a block being processed — useful when the output itself contains `{{ }}` or `{% %}` syntax for a CMS (see the [`@raw` documentation](../language/raw.md))

{% hint style="info" %}
Any files that don't require Elements template language processing should be stored in the [assets](../assets.md) directory instead.
{% endhint %}

## Templates Directory Structure

```
com.yourcompany.component/
├── templates/
│   ├── index.html              # Main component template
│   ├── alpine.html             # Additional template file
│   ├── styles.css              # CSS with template directives
│   ├── include/                # Reusable template partials
│   │   ├── header.html
│   │   ├── footer.html
│   │   └── icon.html
│   └── backend/                # Server-side files
│       └── submit.php
```

### Root-Level Templates

Files placed directly in the `templates/` directory are processed and included for **each instance** of the component on the page. This is where you'll place your component's primary HTML, CSS, and JavaScript.

**Common root-level files:**
- `index.html` - The main component markup (see [index.html documentation](index.html.md))
- Additional HTML files for specific features
- CSS files with template directives (see [CSS Templates](css-templates.md))
- JavaScript files (see [JavaScript Templates](js-templates.md))
- PHP files (see [PHP Templates](php-templates.md))

**Naming conventions used by the core components:**
- `alpine.html` — an HTML template that wraps the component's Alpine.js factory in `@portal(bodyEnd, includeOnce: true, id: "...")` so the script is emitted once per page (see [JavaScript Templates](js-templates.md))
- `editor-ui.css`, `edit.css` — small editor-focused stylesheets; wrap rules in `@if(edit)` to keep them out of the published site (see [CSS Templates](css-templates.md))

These names are conventions, not requirements — every root-level file is processed regardless of its name.

### Subdirectories

The templates directory supports special subdirectories for organizing your code:

| Directory | Purpose | Documentation |
|-----------|---------|---------------|
| `include/` | Reusable template partials accessed via `@include()` | [Include Directory](include.md) |
| `backend/` | Server-side files deployed to the backend directory | [Backend](backend.md) |

## Supported File Types

The templates directory supports multiple file types, all processed through the Elements template engine:

| Extension | Description | Use Case |
|-----------|-------------|----------|
| `.html` | HTML markup | Component structure, content areas |
| `.css` | Stylesheets | Component-specific styles with property insertion |
| `.js` | JavaScript | Interactive behavior with property values |
| `.php` | PHP code | Server-side processing (typically in backend/) |

All these file types can use the full [Elements Language](../language/README.md) syntax, including property insertion, conditionals, and directives.

## Processing Behavior

### Per-Instance Processing

Root-level template files are processed **once per component instance**. If you have three button components on a page, each button's templates are processed independently with its own properties.

### Template Order

Template files are processed in alphabetical order by filename. If order matters for your templates, you can:
- Use the `@portal` directive to inject content into specific page locations
- Combine multiple templates into a single file
- Use naming conventions (e.g., `01-setup.html`, `02-main.html`)

### Property Scope

Templates have access to:
- Component properties defined in `properties.json`
- Data passed from `hooks.js` using `rw.setProps()`
- Built-in properties like `id`, `edit`, `preview`
- Collection data when using `@each`

## Common Patterns

### Portal-Based Templates

Use the `@portal` directive to inject scripts or styles into specific page locations, even though the template is processed per-instance:

```html
@portal(bodyEnd, includeOnce: true, id: "my-component-script")
<script>
    // This script is included only once per page
    Alpine.data("myComponent", () => ({
        // Component logic
    }));
</script>
@endportal
```

See the [`@portal` documentation](../language/portal.md) for more details.

### Conditional Templates

Wrap template content in conditionals for different modes or property values:

```html
@if(edit)
    <div class="edit-mode-placeholder">
        Click to configure this component
    </div>
@else
    <div class="{{classes.container}}">
        @dropzone("content", title: "Content")
    </div>
@endif
```

See the [`@if` documentation](../language/if.md) for more details.

### Template Includes

Break complex components into smaller, reusable pieces:

```html
<!-- templates/index.html -->
<nav class="{{classes.navbar}}">
    @include("logo")
    @include("menu")
</nav>

<!-- templates/include/logo.html -->
<div class="logo">
    {{siteName}}
</div>

<!-- templates/include/menu.html -->
<ul class="menu">
    @each(item in menuItems)
        <li>{{item.title}}</li>
    @endeach
</ul>
```

See the [Include Directory documentation](include.md) and [`@include` directive](../language/include.md) for more details.

## Templates vs Assets

Choose the right location for your files:

**Use `templates/` when:**
- Files need property replacement (e.g., `{{propertyName}}`)
- You need conditional rendering or loops
- Files should be processed per-component instance
- You're using Elements Language directives

**Use `assets/` when:**
- Files are static and don't need processing
- Files are large libraries (Alpine.js, GSAP, etc.)
- Files should be included once per page regardless of instances
- You want optimal caching and performance

## Examples from Core Components

### Simple Component (Typography)

```html
@richtext("content", title: "Typography", default: "Start editing this text...")
```

### Component with Conditionals (Button)

```html
@if(showText)
@text("text", title: "Button Text", default: "Click Me")
@endif
@if(wantsDropzone)
<div class="{{dropzoneSide}}">
  @dropzone("dropzone", title: "Icon")
</div>
@endif
```

### Component with Includes (Gallery)

```html
@if(!hasResources)
    <!-- Placeholder UI -->
@else
<div class="{{classes.wrapper}}" x-data>
    @each(image in resources)
        @include("thumbnail")
    @endeach
</div>
@endif
@includeIf(includeLightbox, template: "lightbox")
```

## Next Steps

Explore the detailed documentation for each template type:

- [index.html](index.html.md) - Learn about the main template file
- [Include Directory](include.md) - Organize reusable template partials
- [CSS Templates](css-templates.md) - Add styles with template directives
- [JavaScript Templates](js-templates.md) - Create interactive behavior
- [PHP Templates](php-templates.md) - Add server-side processing
- [Backend](backend.md) - Deploy files to the server

For template language syntax, see the [Elements Language](../language/README.md) documentation.
