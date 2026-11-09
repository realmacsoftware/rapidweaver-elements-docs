---
description: The main template file for your component
---

# index.html

The `index.html` file is the primary template for your component. It defines the HTML structure, content areas, and markup that will be rendered for each instance of your component on a page.

## Overview

When you create a new component, `templates/index.html` is typically the first (and often only) template file you'll need. It serves as the entry point for your component's visual output and contains the markup that defines how your component appears to users.

## File Location

```
com.yourcompany.component/
├── templates/
│   └── index.html    # Main component template
```

## Basic Structure

A simple `index.html` might look like this:

```html
<div class="{{classes.container}}">
    @text("heading", title: "Heading", default: "Welcome")
    @richtext("content", title: "Content", default: "Start typing...")
</div>
```

## Key Features

### Property Insertion

Access component properties using double curly braces:

```html
<div class="{{customClass}}">
    <h2>{{title}}</h2>
    <p>{{description}}</p>
</div>
```

Properties can come from:

* `properties.json` - User-defined properties
* `hooks.js` - Data passed via `rw.setProps()`
* Built-in properties like `id`, `edit`, `preview`

### Content Areas

Define editable regions using content directives:

```html
<!-- Plain text area -->
@text("label", title: "Button Label", default: "Click Me")

<!-- Rich text with formatting -->
@richtext("content", title: "Body Content")

<!-- Markdown editor -->
@markdown("article", title: "Article")

<!-- Container for child components -->
@dropzone("items", title: "Content Area")
```

See the [Elements Language](../language/) documentation for all available directives.

### Conditional Rendering

Show or hide content based on properties or modes:

```html
@if(edit)
    <div class="edit-placeholder">
        Configure your component in the inspector
    </div>
@elseif(showPlaceholder)
    <div class="placeholder">
        Add content to get started
    </div>
@else
    <div class="{{classes.wrapper}}">
        @dropzone("content", title: "Content")
    </div>
@endif
```

### Loops and Collections

Iterate over collections with `@each`:

```html
<ul class="{{classes.list}}">
    @each(item in items)
        <li class="{{item.classes}}">
            <h3>{{item.title}}</h3>
            <p>{{item.description}}</p>
        </li>
    @endeach
</ul>
```

### Including Partials

Break complex templates into reusable pieces:

```html
<div class="component">
    @include("header")
    
    <div class="content">
        @dropzone("main", title: "Main Content")
    </div>
    
    @include("footer")
</div>
```

Include files are stored in `templates/include/`. See the [Include Directory](include.md) documentation.

## Processing Behavior

### Per-Instance Processing

The `index.html` template is processed **once for each component instance** on the page. If you add three instances of your component, the template runs three times with each instance's unique properties.

```html
<!-- Each button instance gets its own text -->
<button class="{{classes.button}}">
    @text("label", default: "Click Me")
</button>
```

### Output Location

The processed HTML from `index.html` is inserted directly where the component is placed in the page structure. It becomes part of the page's normal flow.

## Common Patterns

### Edit Mode Placeholders

Provide helpful UI when users are editing. Template `@if` accepts a single condition, so compute the combined check in `hooks.js` first. See [Combining Conditions](../language/if.md#combining-conditions).

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { hasContent } = rw.props;
    rw.setProps({ showEmptyState: rw.project.mode === "edit" && !hasContent });
};
```

```html
@if(showEmptyState)
    <div class="empty-state">
        <p>Add content to this component</p>
    </div>
@else
    @dropzone("content", title: "Content")
@endif
```

### Responsive Classes

Use responsive property values for different breakpoints:

```html
<div class="{{classes.container}} {{responsiveClasses}}">
    <!-- Content -->
</div>
```

Properties can be configured as responsive in `properties.json`, and you can access breakpoint-specific values in `hooks.js`.

### Component ID

Use the unique component ID for JavaScript targeting:

```html
<div id="component-{{id}}" data-component="myComponent">
    <!-- Content -->
</div>
```

### Alpine.js Integration

Integrate with Alpine.js for interactive components. Pass structured data through a `data-*` attribute rather than interpolating it directly into the `x-data` expression — see [Data Attributes](js-templates.md#data-attributes) in the JavaScript Templates guide.

```javascript
// hooks.js - serialise structured options at build time
exports.transformHook = (rw) => {
    rw.setProps({ optionsJson: JSON.stringify(rw.props.options ?? {}) });
};
```

```html
<div x-data="myComponent('{{id}}')" data-options='{{optionsJson}}'>
    <button x-on:click="toggle">
        {{buttonLabel}}
    </button>

    <div x-show="isOpen" x-collapse>
        @dropzone("content", title: "Content")
    </div>
</div>
```

{% hint style="warning" %}
**Do not interpolate plain `JSON.stringify` output into `x-data`** (e.g. `x-data="myComponent('{{id}}', {{options}})"`). The JSON's double-quotes terminate the HTML attribute; Alpine fails to parse the expression and the component silently renders blank. Use a single-quoted `data-*` attribute as shown above, or the [quote-swap pattern](js-templates.md#the-quote-swap-pattern) used by the core Table and Content Slider components.
{% endhint %}

## Examples from Core Components

### Simple Component (Typography)

The Typography component has a minimal `index.html`:

```html
@richtext("content", title: "Typography", default: "Elements makes building beautiful websites effortless. With powerful drag-and-drop components, you can create stunning web pages without writing code. Start editing this text to bring your ideas to life.")
```

### Interactive Component (Button)

The Button component uses conditionals to show different content areas:

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

### Complex Component (Gallery)

The Gallery component combines conditionals, loops, and includes:

```html
@if(!hasResources)
<div
    rwResourceDropZone="resources"
    class="col-span-full w-full h-64 flex flex-col items-center justify-center border-2 border-dashed border-gray-300 rounded-xl bg-gray-50 hover:bg-gray-100 transition cursor-pointer text-center px-4 py-6"
>
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-10 h-10 text-gray-700 mb-2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 12.75V12A2.25 2.25 0 0 1 4.5 9.75h15A2.25 2.25 0 0 1 21.75 12v.75m-8.69-6.44-2.12-2.12a1.5 1.5 0 0 0-1.061-.44H4.5A2.25 2.25 0 0 0 2.25 6v12a2.25 2.25 0 0 0 2.25 2.25h15A2.25 2.25 0 0 0 21.75 18V9a2.25 2.25 0 0 0-2.25-2.25h-5.379a1.5 1.5 0 0 1-1.06-.44Z" />
    </svg>
    <p class="text-lg font-medium text-gray-700">
        Drag & drop a folder of resources
    </p>
    <p class="text-sm text-gray-400">or add them via the component inspector</p>
</div>
@else
<div class="{{classes.wrapper}}" x-data>
    @each(image in resources)
        @include("thumbnail")
    @endeach
</div>
@endif
@includeIf(includeLightbox, template: "lightbox")
```

## Best Practices

### Keep It Focused

If your `index.html` becomes large and complex:

* Extract repeated markup into includes
* Move complex logic to `hooks.js`
* Consider breaking the component into smaller components

### Use Semantic HTML

Structure your markup with proper HTML5 elements:

```html
<article class="{{classes.card}}">
    <header>
        <h2>{{title}}</h2>
    </header>
    <div class="content">
        @richtext("body", title: "Content")
    </div>
    <footer>
        @include("metadata")
    </footer>
</article>
```

### Provide Defaults

Always provide sensible default values for text areas:

```html
@text("heading", title: "Heading", default: "Welcome to My Component")
```

This creates a better experience when users first add your component.

### Consider Accessibility

Include proper ARIA attributes and semantic markup:

```html
<button 
    aria-label="{{ariaLabel}}" 
    aria-expanded="{{isExpanded}}"
    class="{{classes.button}}"
>
    {{buttonText}}
</button>
```

## Related Documentation

* [Elements Language](../language/) - Complete template syntax reference
* [Include Directory](include.md) - Reusable template partials
* [Templates Overview](./) - Understanding the templates directory
* [Properties](../properties.json/) - Defining component properties
* [Hooks.js](../hooks.js/) - Passing data to templates
