---
description: Create linkable anchors that appear in the Elements Link Panel
---

# @anchor

The `@anchor` directive creates a linkable anchor point within your component. Anchors defined with this directive automatically appear in the Elements Link Panel, making it easy for users to link to specific sections of your component from anywhere in their project.

## Syntax

Using a literal string:

```html
<div id="@anchor("anchorName")"></div>
```

Using a property value:

```html
<div id="@anchor(anchorProperty)"></div>
```

## How It Works

When you use `@anchor`, Elements:

1. Outputs the anchor name/value as the element's `id` attribute
2. Registers the anchor in the Link Panel so users can select it when creating links
3. Enables smooth scrolling to the anchor when the link is clicked

## Examples

### Basic Anchor

Create a static anchor point:

```html
<section id="@anchor("features")">
    <h2>Features</h2>
    <!-- Section content -->
</section>
```

This creates an anchor called "features" that users can link to via the Link Panel.

### Dynamic Anchor from Property

Allow users to customize the anchor name through a component property:

```html
<div id="@anchor(sectionId)"></div>
```

Where `sectionId` is defined in your properties.json as a text input.

### Multiple Anchors in One Component

Components can define multiple anchor points:

```html
<article>
    <header id="@anchor("header")">
        <h1>{{title}}</h1>
    </header>
    
    <section id="@anchor("content")">
        {{content}}
    </section>
    
    <footer id="@anchor("footer")">
        <!-- Footer content -->
    </footer>
</article>
```

### Accordion Sections

Create anchors for each accordion section:

```html
<div 
    id="@anchor(accordionAnchor)"
    class="accordion-item"
>
    <div class="accordion-header">
        @dropzone("title", title: "Title")
    </div>
    <div class="accordion-content">
        @dropzone("content", title: "Content")
    </div>
</div>
```

### Navigation Target

Create an anchor for a navigation section:

```html
<nav id="@anchor("mainNav")" class="navigation">
    <!-- Navigation items -->
</nav>
```

## Anchors in Hooks File

For more complex anchor scenarios or when anchors need to be generated programmatically, you can use `rw.addAnchor()` in your hooks file instead of the template directive.

```javascript
// In hooks.js
rw.addAnchor({
    id: "custom-anchor",
    title: "Custom Section"
});
```

This is useful when:
- Anchor names need to be computed from multiple properties
- You need to conditionally add anchors based on complex logic
- Anchors need to be added in a loop with dynamic IDs

See [rw.addAnchor](../hooks.js/available-functions/rw.addanchor.md) for more details on the hooks approach.

## Best Practices

1. **Use descriptive anchor names** - Choose names that clearly describe the section: `"pricing"`, `"contact-form"`, `"testimonials"`.

2. **Keep anchor names URL-friendly** - Use lowercase letters, numbers, and hyphens. Avoid spaces and special characters.

3. **Consider user control** - For reusable components, expose the anchor name as a property so users can customize it.

4. **Document your anchors** - If your component creates anchors, document them so users know what links are available.

## Related

- [rw.addAnchor](../hooks.js/available-functions/rw.addanchor.md) - Programmatic anchor creation in hooks file
- [Link UI Control](../properties.json/ui-controls/link.md) - Creating link properties
