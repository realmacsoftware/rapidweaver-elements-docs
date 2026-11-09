---
description: Iterate over collections and arrays to repeat content
---

# @each

The `@each` directive allows you to iterate over arrays and collections, repeating a block of content for each item. This is essential for rendering lists, galleries, navigation menus, and any repeated content patterns.

## Syntax

```html
@each(item in items)
    <!-- Content repeated for each item -->
@endeach
```

The loop variable (e.g., `item`) is scoped to the loop block and provides access to each element in the collection.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `item` | The loop variable name you define to reference the current item |
| `items` | The collection or array to iterate over |

## Loop Variables

Within an `@each` loop, you have access to special loop variables that provide information about the current iteration:

| Variable | Type | Description |
|----------|------|-------------|
| `::index` | Number | The zero-based index of the current item |
| `::isFirst` | Boolean | Returns `true` if this is the first item in the collection |
| `::isLast` | Boolean | Returns `true` if this is the last item in the collection |

These variables are accessed by appending them to your loop variable name (e.g., `image::index`, `page::isFirst`).

## Examples

### Basic List Iteration

```html
@each(item in items)
    <li>{{item.title}}</li>
@endeach
```

### Using Loop Index

Access the current index for numbering or JavaScript interactions:

```html
@each(track in tracks)
    <li x-show="currentTrackIndex === {{track::index}}">
        {{track.title}}
    </li>
@endeach
```

### Conditional Styling with isFirst and isLast

Apply different styles to the first or last items:

```html
@each(image in images.resources)
    <div class="slide @if(image::isFirst) slide-active @else slide-hidden @endif">
        <img src="{{image.image}}" alt="{{image.caption}}" />
    </div>
@endeach
```

### Grid Overlay with First/Last Detection

```html
@each(column in deviceColumns.items)
    @if(column::isFirst)
        <div class="border-r"></div>
    @elseif(column::isLast)
        <div class="border-l"></div>
    @else
        <div class="border-x"></div>
    @endif
@endeach
```

### Navigation Menu Iteration

Iterate over pages and include different templates based on conditions:

```html
<ul>
    @each(page in pages)
        @if(page.isFolder)
            @include("folder_item")
        @else
            @include("link_item")
        @endif
    @endeach
</ul>
```

### Nested Loops

Loop through hierarchical data structures like nested navigation:

```html
@each(page in pages)
    <li>
        <a href="{{page.url}}">{{page.title}}</a>
        @if(page.hasPages)
            <ul>
                @each(subPage in page.pages)
                    <li><a href="{{subPage.url}}">{{subPage.title}}</a></li>
                @endeach
            </ul>
        @endif
    </li>
@endeach
```

### Passing Loop Items to Includes

Pass the current loop item to an include template:

```html
@each(page in pages)
    @include("menu_item", page: page)
@endeach
```

### Gallery with Click Events

Use the loop index for interactive elements:

```html
@each(image in resources)
    <div 
        @click="$dispatch('gallery-show', {index: {{image::index}}})"
        class="thumbnail"
    >
        <img src="{{image.thumbnail}}" alt="{{image.caption}}" />
    </div>
@endeach
```

### Responsive Image Sources

Iterate over responsive image sources:

```html
<picture>
    @each(source in image.sources)
        <source media="{{source.media}}" srcset="{{source.srcset}}" />
    @endeach
    <img src="{{image.fallback}}" alt="{{image.alt}}" />
</picture>
```

## Best Practices

1. **Use meaningful variable names** - Choose descriptive names like `page`, `image`, or `track` rather than generic names like `item` or `i`.

2. **Combine with @if for conditional rendering** - Use loop variables with conditionals for first/last item styling.

3. **Extract complex item markup** - For complex item templates, use `@include` to keep your main template clean.

4. **Access nested properties** - Use dot notation to access nested properties: `{{item.author.name}}`.
