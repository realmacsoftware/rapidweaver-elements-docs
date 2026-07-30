---
description: >-
  Build project-specific components with HTML, CSS, JavaScript, and the Elements
  Language
icon: box-open
---

# Custom Components

Custom Components let you extend RapidWeaver Elements with your own reusable building blocks. Start with a simple HTML snippet, or create a complete component with editable content, drop zones, Inspector controls, custom styles, client-side JavaScript, and build-time hooks.

Everything can be created and edited inside Elements, with changes appearing on the canvas as you work. A basic understanding of HTML is helpful, but you can begin with a small snippet and add more advanced features when you need them.

{% hint style="info" %}
Custom Components use the same [Elements Language](https://docs.realmacsoftware.com/elements-docs/elements-language) that powers Element Packs. They are a practical way to learn the API before moving a component into a distributable pack.
{% endhint %}

### What You Can Create

* Reusable HTML sections for a project.
* Components with editable text and child-component drop zones.
* Inspector controls for colours, fonts, spacing, switches, selections, and other values.
* Interactive components using JavaScript or Alpine.js.
* Components whose properties are processed with build-time hooks.

### Requirements and Limitations

* Custom Components are stored inside the project in which they were created.
* An external code editor is not required.
* A Base licence can create up to three Custom Components per project. Plus and Pro licences allow unlimited Custom Components.
* The built-in editor provides five fixed code areas: Template, Styles, JavaScript, Hooks, and Properties.
* Custom Components cannot bundle extra assets, icons, or additional template files.

When a component needs bundled files, collections, custom icons, several templates, or distribution through the Elements Store, move it into an Element Dev Pack.

{% hint style="warning" %}
Custom HTML, CSS, and JavaScript become part of the published website. Preview the component at every breakpoint and test keyboard use, accessibility, and browser behaviour before publishing.
{% endhint %}

### Start with an HTML Snippet

One of the easiest ways to begin is to add a small HTML component and edit its Template.

{% embed url="https://www.youtube.com/watch?v=rHDCpYrg-j4" %}

### How to Create a Custom Component

{% stepper %}
{% step %}
#### Open the Components Area

In the Components area of the project sidebar, select the **+** button beside **Custom**, then choose **HTML**. The new component appears in the Custom list.

<figure><img src="../../.gitbook/assets/CleanShot 2025-06-01 at 12 .02.15@2x.png" alt="The add button beside the Custom heading in the Components area"><figcaption><p>Create an HTML component from the Custom section.</p></figcaption></figure>
{% endstep %}

{% step %}
#### Add the Component to a Page

Drag the new component from the Components area onto the page.

<figure><img src="../../.gitbook/assets/CleanShot 2025-06-01 at 12 .03.57@2x.png" alt="A newly created HTML component added to an Elements page"><figcaption><p>Add the Custom Component to the page before editing it.</p></figcaption></figure>
{% endstep %}

{% step %}
#### Open the Component Editor

Open the Component Editor and select the Template area. Edit the starter markup and watch the component update on the canvas.

<figure><img src="../../.gitbook/assets/CleanShot 2025-06-01 at 12 .04.38@2x.png" alt="Template code open in the Component Editor"><figcaption><p>Template changes appear on the canvas as you work.</p></figcaption></figure>

The Component Editor is a workspace panel, so it can be placed wherever it suits your layout. Right-click a workspace icon to choose the panel from the menu.

<figure><img src="../../.gitbook/assets/CleanShot 2025-06-01 at 12 .08.23@2x.png" alt="Selecting the Component Editor from a workspace panel menu"><figcaption><p>Add the Component Editor to a convenient part of the workspace.</p></figcaption></figure>
{% endstep %}
{% endstepper %}

### The Component Editor

Every Custom Component contains five built-in areas:

* **Template** — HTML processed by the Elements Language. Add markup, editable content areas, drop zones, and property references here.
* **Styles** — CSS used by the component.
* **JavaScript** — Client-side behaviour that runs in the published page.
* **Hooks** — Build-time JavaScript that reads and transforms component properties before the Template is rendered.
* **Properties** — Configuration for the controls shown in the Inspector.

These areas cannot be renamed, removed, or expanded with extra files inside a Custom Component.

### Add Editable Content

Use `@text` in the Template to create text that can be edited directly on the page:

```html
<h1 class="font-heading text-lg text-gray-300">
    @text("heading", default: "Hello World!")
</h1>
```

The first value is a unique name for the editable area. The optional `default` value is shown when a new instance of the component is added.

Use `@dropzone` when the component should accept other Elements components:

```html
@dropzone("content", title: "Content")
```

Each editable area and drop zone should have a unique, descriptive name within the component.

### Add Inspector Controls

The Properties area defines the controls shown in the Inspector. Give each control an `id`, then insert its formatted value into the Template using `{{id}}`.

This example adds a theme-aware text-colour control:

```json
{
    "groups": [
        {
            "title": "Settings",
            "properties": [
                {
                    "title": "Text Color",
                    "id": "textColor",
                    "format": "text-{{value}}",
                    "themeColor": {
                        "default": {
                            "name": "red",
                            "brightness": 600
                        }
                    }
                }
            ]
        }
    ]
}
```

Use the property in the Template:

```html
<p class="{{textColor}}">Hello World!</p>
```

See the [Properties reference](https://docs.realmacsoftware.com/elements-docs/elements-language/component/properties-json) for the available controls and configuration options.

{% hint style="info" %}
The [Add Snow to Your Website](../../getting-started/how-to/add-snow-to-your-website.md) tutorial is a complete example driven by Amount and Follow Mouse properties.
{% endhint %}

### Add Styles

Elements is built around Tailwind CSS, so utility classes in the Template are the best starting point. Use the Styles area when the design needs CSS that is clearer or more practical as a custom rule.

Include the component instance ID when a rule must not affect other instances:

```css
.component-{{id}} {
    letter-spacing: 0.05em;
}
```

Apply the same class in the Template:

```html
<div class="component-{{id}}">
    @dropzone("content", title: "Content")
</div>
```

### Add JavaScript

Use the JavaScript area for behaviour that runs in the visitor’s browser. Elements also includes Alpine.js for lightweight interactions.

When using Alpine directives in the Template, write event handlers with `x-on:` because the `@` prefix is reserved by the Elements Language:

```html
<button x-on:click="open = !open">Toggle content</button>
```

Keep controls keyboard accessible and avoid adding the same global event listener more than once when several instances appear on a page.

### Transform Values with Hooks

Hooks run at build time in the order **Properties → Hooks → Template**. Read Inspector values from `rw.props`, prepare the values the Template needs, then pass them to the Template with `rw.setProps()`.

```javascript
const transformHook = (rw) => {
    const { firstName, lastName } = rw.props;

    rw.setProps({
        fullName: `${firstName} ${lastName}`
    });
};

exports.transformHook = transformHook;
```

The Template can then use the derived value:

```html
<p>{{fullName}}</p>
```

See the [Hooks reference](https://docs.realmacsoftware.com/elements-docs/elements-language/component/hooks.js) for the complete build-time API.

### Tips and Best Practices

* **Start small:** Get the HTML structure working before adding Properties, JavaScript, or Hooks.
* **Use meaningful names:** Names such as `headingColor` and `content` are easier to maintain than generic identifiers.
* **Prefer theme controls:** Theme-aware colour, font, and spacing properties help the component remain consistent with the project.
* **Scope custom code:** Use `{{id}}` when styles or selectors must apply to one component instance.
* **Design accessibly:** Use semantic HTML, visible focus states, labelled controls, alternative text, and reduced-motion behaviour where appropriate.
* **Test several instances:** Confirm that IDs, scripts, styles, and interactions still work when the component appears more than once.

### Custom Component Workshop

Dan and Ben discuss how Custom Components use properties, resources, drop zones, and hooks, and when to move from a project component to a complete pack.

{% embed url="https://youtu.be/aqOOChtClwI?si=sKpgkAruLBAROR7P" %}

### Move to an Element Pack

Custom Components are ideal for project-specific work and learning the Elements Language. A distributable Element Pack is the next step when a component needs its own files, icons, assets, collections, or release process.

Dev Packs are editable development bundles and should not be sold or distributed directly. Compile finished work into an Element Pack through the Elements Platform before sharing or selling it.

Use the [Element Pack getting-started guide](https://docs.realmacsoftware.com/elements-docs/elements-language/api-introduction/getting-started) to create a pack, then explore the [open-source Core Components](https://docs.realmacsoftware.com/elements-docs/elements-language/dev-resources/open-source-components) for production examples.

### Related Documentation

* [Elements Language](https://docs.realmacsoftware.com/elements-docs/elements-language) — Complete API and template-language documentation.
* [Deep Linking](../url-scheme.md) — Create links that import Custom Components into Elements.
* [Licence Types](../../getting-started/license-types.md) — Compare Custom Component limits and commercial permissions.
