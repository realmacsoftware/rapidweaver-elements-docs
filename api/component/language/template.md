---
description: Define inline reusable template blocks
---

# @template

The `@template` directive allows you to define reusable template blocks inline within your main template file. This is useful for small, component-specific templates that don't warrant separate include files.

## Syntax

```html
@template("templateName")
    <!-- Template content -->
@endtemplate
```

Then use it with `@include`:

```html
@include("templateName")
```

## When to Use @template

Use inline templates when:

- The template is small and only used within the current component
- You want to keep related code together in one file
- Creating a separate include file feels like overkill

For larger or shared templates, consider using [include files](include.md) instead.

## Examples

### Basic Inline Template

Define a template at the start of your file, then use it:

```html
@template("list-item")
    <li>{{item.name}}</li>
@endtemplate

<h1>My List</h1>
<ul>
    @each(item in items)
        @include("list-item")
    @endeach
</ul>
```

### Button Template with Parameters

Create a reusable button pattern:

```html
@template("button")
    <button class="btn {{buttonClass}}">{{label}}</button>
@endtemplate

<div class="actions">
    @include("button", label: "Save", buttonClass: "btn-primary")
    @include("button", label: "Cancel", buttonClass: "btn-secondary")
</div>
```

### Card Template

Define a card layout that's reused multiple times:

```html
@template("card")
    <div class="card">
        <div class="card-header">{{title}}</div>
        <div class="card-body">{{content}}</div>
    </div>
@endtemplate

<div class="grid">
    @each(item in cards)
        @include("card", title: item.title, content: item.description)
    @endeach
</div>
```

### Icon Template

Create a reusable icon wrapper:

```html
@template("icon")
    <span class="icon icon-{{name}}" aria-hidden="true">
        {{svg}}
    </span>
@endtemplate

<nav>
    @include("icon", name: "home", svg: homeSvg)
    @include("icon", name: "settings", svg: settingsSvg)
</nav>
```

### Alert Template

Define different alert styles:

```html
@template("alert")
    <div class="alert alert-{{type}}" role="alert">
        <strong>{{title}}</strong>
        <p>{{message}}</p>
    </div>
@endtemplate

@if(hasError)
    @include("alert", type: "error", title: "Error", message: errorMessage)
@endif

@if(hasSuccess)
    @include("alert", type: "success", title: "Success", message: successMessage)
@endif
```

## Template Placement

Templates should be defined at the **beginning** of your template file, before any HTML output. This keeps your templates organized and makes them easy to find:

```html
<!-- Define templates first -->
@template("header")
    <header>{{title}}</header>
@endtemplate

@template("footer")
    <footer>{{copyright}}</footer>
@endtemplate

<!-- Then your main template content -->
<div class="page">
    @include("header", title: pageTitle)
    
    <main>
        @dropzone("content")
    </main>
    
    @include("footer", copyright: copyrightText)
</div>
```

## Scope and Properties

Inline templates have access to:

1. **Properties passed via @include** - Explicitly passed values take precedence
2. **Parent template properties** - All properties from the parent template are accessible
3. **Loop context** - When included inside an `@each` loop, the loop variable is available

### Example with Scope

```html
@template("item")
    <!-- 'item' comes from the @each loop -->
    <!-- 'highlightClass' comes from the parent template properties -->
    <li class="{{highlightClass}}">{{item.name}}</li>
@endtemplate

@each(item in items)
    @include("item")
@endeach
```

## Best Practices

1. **Keep templates small** - If a template grows large, move it to an include file.

2. **Define templates at the top** - Place all `@template` definitions before your main content.

3. **Use descriptive names** - Name templates after their purpose: `"list-item"`, `"card"`, `"button"`.

4. **Pass explicit properties when possible** - This makes the template's dependencies clear.

5. **Don't nest template definitions** - Define templates at the top level, not inside other blocks.

## Related

- [@include](include.md) - Including external template files
- [@each](each.md) - Looping over collections
