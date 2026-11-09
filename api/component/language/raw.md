---
description: Disable template processing for a section of content
---

# @raw

The `@raw` directive prevents the Elements template engine from processing content within its block. This is essential when you need to output literal `{{` and `}}` syntax, such as when integrating with external templating systems like Elements CMS or JavaScript templating libraries.

## Syntax

```html
@raw()
    <!-- Content here will not be processed by Elements -->
@endraw
```

## Use Cases

### Elements CMS Integration

When using Elements CMS, you need to output CMS template syntax that uses the same `{{}}` delimiters as the Elements templating language. Wrap CMS-specific code in `@raw` to prevent Elements from processing it:

```html
@raw()
    <div class="text-sm text-black-600">{{item.title}}</div>
@endraw
```

Without `@raw`, Elements would try to find a property called `item.title` and replace it. With `@raw`, the literal text `{{item.title}}` is output for the CMS to process at runtime.

### CMS Loop Syntax

Preserve CMS loop syntax in your templates:

```html
@raw()
    {% for image in item.gallery %}
        <img src="{{image.src}}" alt="{{image.alt}}" />
    {% endfor %}
@endraw
```

### Mixing Elements and CMS Syntax

You can exit and re-enter `@raw` blocks to mix Elements properties with CMS syntax:

```html
@each(image in images.resources)
    <div class="slide">
        <img src="{{image.image}}" />
    </div>
@endeach

@else

@raw()
    {% for image in item.@endraw{{cmsField}}@raw() %}
        <div class="slide">
            <img src="{{image.src}}" />
        </div>
    {% endfor %}
@endraw
```

In this example:
- Elements processes `{{cmsField}}` to insert the field name
- The CMS processes the rest at runtime

### JavaScript Template Literals

When using JavaScript templating libraries that use similar syntax:

```html
@raw()
    <script type="text/template" id="my-template">
        <div class="item">
            <h2>{{title}}</h2>
            <p>{{description}}</p>
        </div>
    </script>
@endraw
```

### Vue.js or Similar Frameworks

Preserve Vue.js mustache syntax:

```html
@raw()
    <div id="app">
        <p>{{ message }}</p>
        <ul>
            <li v-for="item in items">{{ item.name }}</li>
        </ul>
    </div>
@endraw
```

## Combining with Elements Properties

You can use Elements properties outside `@raw` blocks to inject dynamic values into CMS templates:

```html
<div class="{{classes.wrapper}}">
    @raw()
        {% for item in collection %}
            <article class="@endraw{{classes.item}}@raw()">
                <h2>{{item.title}}</h2>
            </article>
        {% endfor %}
    @endraw
</div>
```

This outputs:
- `{{classes.wrapper}}` - Replaced by Elements with the actual class names
- `{{classes.item}}` - Also replaced by Elements
- `{{item.title}}` - Preserved literally for CMS processing

## Best Practices

1. **Use for external templating only** - Only use `@raw` when integrating with external systems that use `{{}}` syntax.

2. **Keep raw blocks focused** - Include only the content that needs to be preserved; exit `@raw` when you need Elements processing.

3. **Document CMS dependencies** - When your component uses `@raw` for CMS integration, document this clearly for users.

4. **Test both modes** - Test your component with and without CMS data to ensure proper fallback behavior.

## Related

- [Elements CMS Documentation](https://app.gitbook.com/o/qIywZyO82bvjWx2b4aH7/s/Tf3DR4s6R7zTFZDxsRx4/) - External CMS integration
