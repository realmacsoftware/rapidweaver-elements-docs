---
description: Using JavaScript files in the templates directory with template directives
---

# JavaScript Templates

JavaScript files placed in the `templates/` directory are processed through the Elements template engine, allowing you to inject component properties, conditionals, and dynamic values directly into your JavaScript code. This enables you to create interactive components with configuration driven by user properties.

## Overview

JavaScript template files provide:

* **Property insertion** - Use component properties in JavaScript code
* **Conditional code** - Include or exclude JavaScript based on conditions
* **Per-instance configuration** - Each component instance gets its own configuration
* **Portal injection** - Place scripts in specific page locations using `@portal` (from an HTML template)

{% hint style="info" %}
**How the core components ship JavaScript:** every core component keeps its script inside an **HTML template** — conventionally `templates/alpine.html` — wrapped in `@portal(bodyEnd, includeOnce: true)` (usually with a reverse-DNS `id`) so the script lands at the end of `<body>` exactly once, no matter how many instances are on the page. Bare `.js` template files are also supported (they're processed and inserted inline within `<script>` tags), but an `.html` template is the right home for anything that needs the `<script>` tag or portal markup itself.
{% endhint %}

## File Location

```
com.yourcompany.component/
├── templates/
│   ├── index.html
│   ├── alpine.html       # Portal-wrapped <script> (core convention)
│   ├── script.js         # Bare JavaScript template (also supported)
│   └── include/
│       └── ...
```

## Basic Usage

JavaScript files can use standard JavaScript syntax along with Elements template directives:

```javascript
// Initialize component with properties
const component = document.getElementById('component-{{id}}');
component.setAttribute('data-color', '{{color}}');
component.setAttribute('data-enabled', '{{enabled}}');

@if(autoStart)
// Auto-start functionality
component.classList.add('active');
@endif
```

## Property Insertion

Insert component properties directly into JavaScript values:

```javascript
// String values
const componentId = '{{id}}';
const title = '{{title}}';
const description = '{{description}}';

// Numeric values
const duration = {{duration}};
const delay = {{delay}};
const maxItems = {{maxItems}};

// Boolean values (be careful with JSON format)
const isEnabled = {{enabled}};  // true or false
const autoPlay = {{autoPlay}};

// Object properties
const settings = {
    color: '{{color}}',
    size: {{size}},
    animated: {{animated}}
};
```

## Portal Injection

A common pattern is to use `@portal` to inject JavaScript into specific page locations, typically `bodyEnd`. Because the block contains `<script>` markup, it belongs in an `.html` template file (such as `templates/alpine.html`), not a `.js` file:

```html
<!-- templates/alpine.html -->
@portal(bodyEnd, includeOnce: true, id: "my-component-lib")
<script>
    // This script is included only once per page
    window.MyComponent = {
        init: function(id, options) {
            // Component initialization logic
        }
    };
</script>
@endportal
```

Then in your HTML template:

```html
<div id="component-{{id}}" data-component="myComponent">
    <!-- Component markup -->
</div>

<script>
    MyComponent.init('{{id}}', {
        color: '{{color}}',
        autoStart: {{autoStart}}
    });
</script>
```

See the [`@portal` documentation](../language/portal.md) for more details.

## Examples from Core Components

### Accordion Component (Alpine.js)

The Accordion's `templates/alpine.html` uses a portal to define the Alpine.js component logic once:

```html
<!-- templates/alpine.html -->
@portal(bodyEnd, includeOnce: true, id: "com.realmacsoftware.accordion.alpine")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("accordion", (id, options = {}) => ({
            open: options.openOnLoad || false,
            id,
            options,
            init() {
                this.$watch("open", (value) => {
                    if (value && this.options.groupId) {
                        this.$dispatch("close-accordions-in-group", {
                            groupId: this.options.groupId,
                            id: this.id,
                        });
                    }
                });
            },

            details: {
                ["@close-accordions-in-group.window"](e) {
                    const { groupId, id } = e.detail;
                    if (groupId == this.options.groupId && id != this.id) {
                        this.open = false;
                    }
                },
                [":data-open"]() {
                    return this.open.toString();
                },
            },

            summary: {
                ["@click"]() {
                    this.open = !this.open;
                },
            },

            content: {
                ["x-show"]() {
                    return this.open;
                },
            },
        }));
    });
</script>
@endportal
```

Each accordion instance then uses this component with its own properties:

```html
<div x-data="accordion('{{id}}', { openOnLoad: {{openOnLoad}}, groupId: '{{groupId}}' })">
    <!-- Accordion markup -->
</div>
```

### Gallery Component (Lightbox)

The Gallery registers its lightbox as an Alpine.js factory in a root-level template, `templates/alpine-gallery-lightbox.html`:

```html
<!-- templates/alpine-gallery-lightbox.html -->
@portal("bodyEnd", id: "com.realmacsoftware.alpine.gallery-lightbox", includeOnce: true)
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("galleryLightbox", (id = null, options = {}) => ({
            id,
            show: false,
            atBeginning: false,
            atEnd: false,

            init() {
                this.setupKeyboardControls();
                this.setupEventListeners();
            },

            // Keyboard, scroll, and navigation handling...
        }));
    });
</script>
@endportal
```

The lightbox markup in `templates/include/lightbox.html` then binds each instance to the factory:

```html
<div x-data="galleryLightbox('{{id}}')">
    <!-- Lightbox markup -->
</div>
```

Note the portal target can be written quoted (`@portal("bodyEnd", ...)`) or bare (`@portal(bodyEnd, ...)`) — both forms appear in the core components.

## Conditional JavaScript

Use `@if` directives to conditionally include code. Template `@if` accepts a single condition only — boolean properties like `enableLogging` work directly, but comparisons must be computed in `hooks.js` first. See [Combining Conditions](../language/if.md#combining-conditions).

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { animation } = rw.props;
    rw.setProps({
        animationIsFade: animation === "fade",
        animationIsSlide: animation === "slide",
    });
};
```

```javascript
const component = document.getElementById('{{id}}');

@if(enableLogging)
console.log('Component {{id}} initialized with:', {
    color: '{{color}}',
    size: {{size}}
});
@endif

@if(trackAnalytics)
// Send analytics event
analytics.track('component_loaded', {
    componentType: '{{componentType}}',
    componentId: '{{id}}'
});
@endif

@if(animationIsFade)
component.classList.add('fade-animation');
@elseif(animationIsSlide)
component.classList.add('slide-animation');
@else
component.classList.add('no-animation');
@endif
```

## Processing Behavior

### Per-Instance Processing

JavaScript template files are processed **once per component instance**. Each instance gets its own `<script>` tag with processed code:

```javascript
// Instance 1
const comp1 = document.getElementById('component-abc123');
comp1.config = { color: 'blue' };

// Instance 2
const comp2 = document.getElementById('component-def456');
comp2.config = { color: 'red' };
```

### Inline Scripts

Processed JavaScript is inserted inline into the page within `<script>` tags, not as external files.

## Templates vs Assets

Choose the right location for your JavaScript:

### Use `templates/` JavaScript When:

* Code needs component property values
* Code is instance-specific
* Code needs conditional logic
* Configuration varies per instance

**Example:**

```javascript
const instance = new Component('{{id}}', {
    color: '{{userColor}}',
    speed: {{userSpeed}},
    enabled: {{enabled}}
});
```

### Use `assets/` JavaScript When:

* Code is static library code
* Code is shared across all instances
* Code is a large framework (Alpine.js, GSAP, etc.)
* You want better caching and performance

**Example:**

```javascript
// Reusable component class
class Component {
    constructor(id, options) {
        this.id = id;
        this.options = options;
    }
    // Component methods...
}
```

### Combining Both

A common pattern is to define classes in `assets/` and instantiate them in `templates/`:

```
components/
├── assets/
│   └── component-class.js    # Static class definition
└── templates/
    └── init.js               # Per-instance initialization
```

## Best Practices

### Use includeOnce for Libraries

When defining reusable functions or classes, use `includeOnce`:

```html
<!-- templates/alpine.html -->
@portal(bodyEnd, includeOnce: true, id: "my-component-lib")
<script>
    // Define once for the entire page
    class MyComponent {
        // Class definition
    }
    window.MyComponent = MyComponent;
</script>
@endportal
```

### Avoid Inline Event Handlers

Instead of inline handlers in HTML:

```html
<!-- Avoid -->
<button onclick="handleClick('{{id}}', {{someValue}})">
```

Use proper event listeners in JavaScript:

```javascript
document.getElementById('button-{{id}}').addEventListener('click', function() {
    handleClick('{{id}}', {{someValue}});
});
```

### Escape String Values

Be careful with user-provided strings that might contain quotes:

```javascript
// Unsafe
const title = '{{title}}';  // Breaks if title contains '

// Better - use JSON encoding in hooks.js
const title = {{titleJSON}};
```

In `hooks.js`:

```javascript
rw.setProps({
    titleJSON: JSON.stringify(rw.props.title)
});
```

### Minimize Template JavaScript

Keep template JavaScript minimal and focused on configuration:

```javascript
// Good - just configuration
new MyComponent('{{id}}', {
    color: '{{color}}',
    size: {{size}}
});

// Better in assets/ - complex logic
class MyComponent {
    constructor(id, options) {
        // Complex implementation
    }
}
```

### Use Proper Scope

Avoid polluting global scope:

```javascript
// Avoid
function myFunction() {
    // Global function
}

// Better - use IIFE
(function() {
    const component = document.getElementById('{{id}}');
    // Component-specific code
})();

// Or use modern modules
{
    const component = document.getElementById('{{id}}');
    // Block-scoped code
}
```

### Handle Timing

Ensure DOM is ready before accessing elements:

```javascript
@if(edit)
// In edit mode, run immediately
const component = document.getElementById('{{id}}');
component.init();
@else
// In published mode, wait for DOM
document.addEventListener('DOMContentLoaded', function() {
    const component = document.getElementById('{{id}}');
    component.init();
});
@endif
```

## Common Patterns

### Alpine.js Integration

Define Alpine components with property-based configuration:

```html
<!-- templates/alpine.html -->
@portal(bodyEnd, includeOnce: true, id: "my-alpine-component")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("myComponent", (id, config) => ({
            id,
            config,
            // Component state and methods
            init() {
                // Initialization
            }
        }));
    });
</script>
@endportal
```

```html
<div x-data="myComponent('{{id}}', {
    color: '{{color}}',
    autoStart: {{autoStart}}
})">
    <!-- Component markup -->
</div>
```

Registering inside `alpine:init` is required for browser/publish parity. In the edit canvas Alpine may already be initialised when the script runs, so a bare `Alpine.data(...)` call can appear to work — but in a browser the factory must exist before Alpine parses `x-data` attributes, which means it must be registered before `alpine:init` fires. Always use this pattern.

{% hint style="warning" %}
**Don't interpolate raw JSON into the `x-data` expression** (e.g. `x-data="factory('{{id}}', {{dataJson}})"` where `dataJson` is plain `JSON.stringify` output). The JSON's double-quotes terminate the HTML attribute, Alpine fails to parse the expression, and the component silently renders blank. Two working patterns:

1. **Data attributes (recommended)** — pass the JSON through a single-quoted `data-*` attribute and read it with `JSON.parse` in the factory. See [Data Attributes](#data-attributes).
2. **Quote-swap** — used by the core Table and Content Slider components: swap the JSON's double-quotes for single-quotes in `hooks.js` before interpolating. See below.
{% endhint %}

#### The Quote-Swap Pattern

The Content Slider builds its Swiper config in `hooks.js` and swaps the JSON's double-quotes for single-quotes so the value survives inside the double-quoted `x-data` attribute:

```javascript
// hooks.js
const transformHook = (rw) => {
    const swiperOptions = {
        loop: true,
        slidesPerView: 1,
        speed: 400,
    };

    rw.setProps({
        swiperOptions: JSON.stringify(swiperOptions).replace(/"/g, "'"),
    });
};
exports.transformHook = transformHook;
```

```html
<!-- templates/index.html -->
<div x-data="elementsContentSlider('{{id}}', {{swiperOptions}})">
```

This works because Alpine evaluates `x-data` as a JavaScript expression, and the single-quoted output (`{'loop': true, ...}`) is a valid object literal. The Table component defensively handles a string arriving instead, converting the quotes back before parsing:

```javascript
Alpine.data("elementsTable", (id, config) => ({
    config: typeof config === "string" ? JSON.parse(config.replace(/'/g, '"')) : config,
    // ...
}));
```

The caveat: the quote-swap corrupts data that itself contains quote characters, so reserve it for config objects whose values you control. For user-entered content, use a `data-*` attribute instead.

### GSAP Animations

Configure GSAP animations with user properties:

```javascript
@if(enableAnimation)
gsap.to('#component-{{id}}', {
    duration: {{duration}},
    opacity: {{targetOpacity}},
    x: {{translateX}},
    ease: '{{easing}}'
});
@endif
```

### Data Attributes

Set data attributes for JavaScript access:

```javascript
const element = document.getElementById('{{id}}');
element.dataset.componentId = '{{id}}';
element.dataset.variant = '{{variant}}';
element.dataset.enabled = '{{enabled}}';

// Later access
const variant = element.dataset.variant;
```

**Passing structured data (objects/arrays) from `hooks.js`**

For structured data, serialise it in `hooks.js` and embed it in a single-quoted `data-*` attribute. A single-quoted attribute keeps JSON's double-quotes intact; putting them inside a double-quoted `x-data` attribute breaks the HTML parse.

```javascript
// hooks.js
exports.transformHook = (rw) => {
    rw.setProps({ scheduleJson: JSON.stringify(rw.props.schedule ?? {}) });
};
```

```html
<!-- templates/index.html: single-quoted attribute keeps JSON's double-quotes intact -->
<div x-data="openStatus('{{id}}')" data-schedule='{{scheduleJson}}'></div>
```

```html
<!-- templates/alpine.html: read and parse inside factory init() -->
@portal(bodyEnd, includeOnce: true, id: "com.yourname.openstatus.alpine")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("openStatus", (id) => ({
            id,
            schedule: null,
            init() {
                try {
                    this.schedule = JSON.parse(this.$el.dataset.schedule || "null");
                } catch (e) {
                    console.warn("openStatus: invalid schedule JSON", e);
                }
            }
        }));
    });
</script>
@endportal
```

Because `{{ }}` inserts values verbatim (see [Escape String Values](#escape-string-values)), entity-encode `'`, `&`, and `<` in `hooks.js` if the data may contain those characters.

## Limitations

### No ES Modules

Template JavaScript doesn't support ES module syntax:

```javascript
// This won't work in template files
import { something } from './module.js';
export default MyComponent;

// Use traditional scripts or put modules in assets/
```

### Limited Preprocessing

Template JavaScript files don't support TypeScript, Babel, or other preprocessors. Use the Elements template language for logic.

### Execution Context

Template JavaScript runs in the page context, not in a controlled environment. Ensure code is safe and handles errors appropriately.

## Related Documentation

* [Elements Language](../language/) - Template syntax reference
* [`@portal` Directive](../language/portal.md) - Injecting scripts to page locations
* [Templates Overview](./) - Understanding templates
* [Assets](../assets.md) - Static JavaScript files
* [Hooks.js](../hooks.js/) - Preparing data for JavaScript
* [Interactive Components with Alpine.js](../../guides/interactive-components-with-alpine.md) - The full guide to Alpine-driven components
* [Integrating JavaScript Libraries](../../guides/integrating-javascript-libraries.md) - Shipping third-party libraries with components
