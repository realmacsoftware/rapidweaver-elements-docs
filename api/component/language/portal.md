---
description: Transport content to different areas of the page
---

# @portal

The `@portal` directive allows you to transport sections of your template code to another part of the page. This is essential for injecting scripts, styles, or content into specific locations like the page head or body, regardless of where your component appears in the document.

## Syntax

```html
@portal(destination)
    <!-- Content to transport -->
@endportal
```

With additional parameters:

```html
@portal(destination, id: "unique-id", includeOnce: true)
    <!-- Content included only once -->
@endportal
```

The destination can be written bare (`@portal(bodyEnd)`) or quoted (`@portal("bodyEnd")`) — both forms are equivalent, and both appear in the core components.

## Portal Destinations

| Destination | Description |
|-------------|-------------|
| `pageStart` | Before the opening `<html>` tag |
| `pageEnd` | After the closing `</html>` tag |
| `headStart` | At the start of the `<head>` element |
| `headEnd` | At the end of the `<head>` element |
| `bodyStart` | At the start of the `<body>` element |
| `bodyEnd` | At the end of the `<body>` element |

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `destination` | Yes | The target location for the content (see destinations table) |
| `id` | No | A unique identifier for deduplication across multiple components |
| `includeOnce` | No | When `true`, ensures the content is only included once per page |

## Examples

### Injecting Scripts at Body End

The most common use case is injecting JavaScript at the end of the body:

```html
@portal(bodyEnd)
    <script>
        console.log("Component initialized");
    </script>
@endportal
```

### Include Once for Libraries

When including shared libraries like Alpine.js, use `includeOnce` to prevent duplicate includes when multiple instances of your component exist on the page:

```html
@portal(bodyEnd, includeOnce: true)
    <script src="https://cdn.example.com/library.js"></script>
@endportal
```

### Unique ID for Cross-Component Deduplication

When multiple different components might include the same library, use a consistent `id` to deduplicate across all of them:

```html
@portal(bodyEnd, id: "com.realmacsoftware.alpine", includeOnce: true)
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
@endportal
```

### Alpine.js Component Registration

Register Alpine.js components that your element depends on:

```html
@portal(bodyEnd, id: "com.realmacsoftware.accordion.alpine", includeOnce: true)
    <script>
        document.addEventListener("alpine:init", () => {
            Alpine.data("accordion", () => ({
                open: false,
                toggle() {
                    this.open = !this.open;
                }
            }));
        });
    </script>
@endportal
```

### Mobile Menu at Body Start

Transport a mobile navigation overlay to the start of the body:

```html
@if(includeMobileMenu)
    @portal("bodyStart")
        <div x-data="mobileMenu" class="mobile-overlay">
            <!-- Mobile menu content -->
        </div>
    @endportal
@endif
```

### Preload Critical Resources

Add preload hints to the head for performance optimization:

```html
@portal(headStart)
    {{globalBgImageFetchPriorityLinkElement}}
@endportal
```

### Custom Styles in Head

Inject component-specific styles into the page head:

```html
@portal(headEnd, includeOnce: true)
    <style>
        .my-component {
            /* Component styles */
        }
    </style>
@endportal
```

### Modal Dialogs at Body End

Transport modal dialog markup to the end of the body for proper stacking:

```html
@portal("bodyEnd")
    <div x-dialog class="modal-backdrop">
        <div class="modal-content">
            @dropzone("content", title: "Content")
        </div>
    </div>
@endportal
```

## Best Practices

1. **Use `includeOnce` for shared resources** - Always use `includeOnce: true` when including libraries or scripts that should only appear once on the page.

2. **Use consistent IDs across components** - When multiple components might include the same resource, use the same `id` to ensure proper deduplication.

3. **Prefer `bodyEnd` for scripts** - Loading scripts at the end of the body improves page load performance.

4. **Use reverse domain notation for IDs** - Follow the pattern `com.yourcompany.feature` to avoid ID collisions.

5. **Combine with conditionals** - Use `@if` to conditionally include portal content based on component settings.

## Related Documentation

* [Modals, Overlays & Portals](../../guides/modals-overlays-and-portals.md) - Overlay components built on @portal
* [Interactive Components with Alpine.js](../../guides/interactive-components-with-alpine.md) - Registering Alpine factories via portals
* [Integrating JavaScript Libraries](../../guides/integrating-javascript-libraries.md) - Loading libraries exactly once with includeOnce
