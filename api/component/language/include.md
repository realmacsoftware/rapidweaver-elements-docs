---
description: Include content from another template file
---

# @include

The `@include` directive allows you to insert the content of another template file within the current template. This promotes code reuse, keeps templates organized, and makes complex components more maintainable.

## Syntax

```html
@include("templateName")
```

With parameters:

```html
@include("templateName", property1: value1, property2: value2)
```

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `template` | Yes | The name of the template file to include (without `.html` extension) |
| `...properties` | No | Additional properties to pass to the included template |

## File Location

Include files should be stored in the `templates/include/` directory within your component:

```
com.yourcompany.component/
├── templates/
│   ├── index.html
│   └── include/
│       ├── header.html
│       ├── footer.html
│       └── item.html
```

`@include()` resolves **only** files in `templates/include/` — root-level template files can't be included by name, and a call that doesn't match a file in `include/` **fails silently**. Root-level templates never need including: every file at the root of `templates/` is processed automatically (see [Templates](../templates/README.md#root-level-templates)).

## Examples

### Basic Include

Include a template file:

```html
@include("header")
@include("footer")
```

If `header.html` contains `Hello` and `footer.html` contains `World`, the output would be:

```
Hello World
```

### Passing Properties

Pass data to the included template:

```html
@include("button", label: "Buy Now", style: "primary")
```

In the `button.html` template, you can access these as `{{label}}` and `{{style}}`.

### String and Variable Properties

Pass both literal strings and variable values:

```html
@include("banner", title: "Can be a string", body: canAlsoBeAVariable)
```

### Passing Loop Items

Pass the current loop item to an include:

```html
@each(page in pages)
    @include("menu_item", page: page)
@endeach
```

### Navigation with Nested Includes

Build complex navigation with recursive includes:

```html
<!-- In index.html -->
<nav>
    <ul>
        @each(page in pages)
            @include("desktop_item")
        @endeach
    </ul>
</nav>
```

```html
<!-- In include/desktop_item.html -->
@if(page.isFolder)
    @include("desktop_folder")
@else
    <a href="{{page.url}}">{{page.title}}</a>
@endif
```

### Recursive Includes

For hierarchical data like nested menus, templates can include themselves:

```html
<!-- In include/item.html -->
<li>
    <a href="{{page.url}}">{{page.title}}</a>
    @if(page.hasPages)
        <ul>
            @each(subPage in page.pages)
                @include("item", page: subPage)
            @endeach
        </ul>
    @endif
</li>
```

### Gallery Thumbnails

Extract repeated item markup into includes:

```html
<div class="gallery">
    @each(image in resources)
        @include("thumbnail")
    @endeach
</div>
```

## Conditional Includes

### Using @includeIf

Rather than wrapping your `@include` statement inside an `@if` statement, use the `@includeIf` helper for cleaner syntax:

```html
<!-- Instead of this: -->
@if(myVariable)
    @include("myTemplate")
@endif

<!-- Use this: -->
@includeIf(myVariable, template: "myTemplate")
```

### Negating the Condition

You can negate the condition with `!`:

```html
@includeIf(!myVariable, template: "myTemplate")
```

### Real-World Examples

Include a lightbox only when enabled:

```html
@includeIf(wantsLightbox, template: "lightbox")
```

Include video templates based on video type:

```html
@includeIf(bgVideo.isYoutube, template: "youtube")
@includeIf(bgVideo.isVimeo, template: "vimeo")
@includeIf(bgVideo.isMP4, template: "mp4")
```

Include icon only when no custom icon is set:

```html
@includeIf(!hasAnIcon, template: "chevron")
```

Include submenu indicators for pages with children:

```html
<a href="{{page.url}}">
    {{page.title}}
    @includeIf(page.hasPages, template: "submenu_indicator")
</a>
```

## Property Access in Includes

Included templates have access to:

1. **All parent template properties** - Properties from the main template are accessible
2. **Passed properties** - Properties explicitly passed in the include statement
3. **Loop context** - When inside an `@each` loop, the loop variable is accessible

## Best Practices

1. **Extract reusable patterns** - If you find yourself repeating markup, extract it into an include.

2. **Use meaningful file names** - Name include files after their purpose: `button.html`, `menu_item.html`, `lightbox.html`.

3. **Pass only what's needed** - Pass specific properties rather than relying on parent scope when possible.

4. **Use @includeIf for conditionals** - It's cleaner than wrapping includes in if statements.

5. **Organize complex includes** - For components with many includes, group related partials with filename prefixes (e.g. `desktop_*`, `mobile_*`), as the core Navbar component does.

## Related

- [@template](template.md) - For inline template definitions
- [@if](if.md) - For conditional rendering
- [@each](each.md) - For iterating over collections