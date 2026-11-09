---
description: Scaffold the FAQ component, define its inspector controls, and render a static themed accordion
---

# Part 1: Scaffolding & Properties

In this part you'll create the `com.example.faq` component from nothing: an `info.json` that tells Elements what the component is, a `properties.json` that defines every inspector control the finished FAQ will need, a minimal `hooks.js` that turns those controls into Tailwind classes, and a static template with two hard-coded questions so you can see the styling work. The questions become real data in [Part 2](part-2-collections-and-dropzones.md).

## Create the Component Folder

If you don't have a Dev Pack yet, create one from Elements' Addons settings—the [Quickstart](../../getting-started/getting-started.md) walks through it with short videos, including how to install the pack and open its files in your editor.

Inside your pack's `components/` folder, create a new folder named `com.example.faq` with a `templates/` subfolder. By the end of this part it will contain four files:

```
com.example.faq/
├── info.json
├── properties.json
├── hooks.js
└── templates/
    └── index.html
```

Elements watches Dev Pack folders, so every file you save below shows up in the app straight away—keep a page with the component open while you work.

## info.json

The [info.json](../../component/info.json.md) file is the component's manifest. Create it with the following content:

```json
{
    "identifier": "com.example.faq",
    "author": "Example Developer",
    "title": "FAQ",
    "group": "Interactive",
    "tags": ["faq", "accordion", "questions"]
}
```

Key by key:

* `identifier` — the unique ID for the component, in reverse-DNS format: lowercase characters and periods, no spaces. Matching the folder name to the identifier keeps packs easy to navigate; every core component follows this convention.
* `author` — your name or company name.
* `title` — the name shown inside Elements. Keep it short; long titles get truncated in the UI.
* `group` — one of the pre-defined categories that Elements uses to group components in the picker. The [category table](../../component/info.json.md#component-categories) lists **Interactive** as the home of "Modals, Popovers, Accordions, Carousels"—exactly where an FAQ accordion belongs. It's also the group the core Accordion and Tabs components use.
* `tags` — optional keywords that help users find the component.

## properties.json

The [properties.json](../../component/properties.json/README.md) file defines the inspector UI. We'll build it up as three [groups](../../component/properties.json/grouping-controls.md)—Content, Style, and Behavior—each rendered as its own section in the inspector. Group icons use SF Symbol names.

### The Content Group

For now the content is a single heading above the questions, using a [Text](../../component/properties.json/ui-controls/text.md) control:

```json
{
    "title": "Content",
    "icon": "textformat",
    "properties": [
        {
            "title": "Heading",
            "id": "heading",
            "responsive": false,
            "text": {
                "default": "Frequently Asked Questions",
                "placeholder": "Section heading"
            }
        }
    ]
}
```

The `id` is how you'll reference the value everywhere else—`{{heading}}` in templates, `rw.props.heading` in hooks. Part 2 adds the `questions` collection to this same group.

### The Style Group

Styling controls should be theme controls wherever possible, so the component adapts to whatever theme the user picks—this is the central idea of [Component Styling](../../component/component-styling.md). Where a control returns a raw token, the [`format`](../../component/properties.json/general-structure/format.md) key wraps it into a finished Tailwind utility class:

```json
{
    "title": "Style",
    "icon": "paintpalette",
    "properties": [
        {
            "title": "Accent",
            "id": "accentColor",
            "format": "text-{{value}}",
            "themeColor": {
                "default": { "name": "brand", "brightness": 500 }
            }
        },
        { "divider": {} },
        {
            "title": "Item Gap",
            "id": "itemGap",
            "format": "gap-y-{{value}}",
            "themeSpacing": {
                "mode": "single",
                "default": { "base": { "value": "4" } }
            }
        },
        {
            "title": "Corner Radius",
            "id": "itemRadius",
            "themeBorderRadius": {
                "default": { "base": { "value": "lg" } }
            }
        },
        { "divider": {} },
        {
            "title": "Question Size",
            "id": "questionTextStyle",
            "themeTextStyle": {
                "default": { "base": { "name": "lg" } }
            }
        }
    ]
}
```

What each control emits:

* **Accent** — a [Theme Color](../../component/properties.json/ui-controls/theme-color.md) returns a `name-brightness` token like `brand-500`; the `format` turns it into `text-brand-500`. It colors the question text — and, because the open/close indicator sits inside the question button, the indicator inherits it too.
* **Item Gap** — a [Theme Spacing](../../component/properties.json/ui-controls/theme-spacing.md) control in `single` mode returns one value from the theme's spacing scale; formatted as `gap-y-{{value}}` it yields `gap-y-4`, the vertical gap between FAQ items.
* **Corner Radius** — a [Theme Border Radius](../../component/properties.json/ui-controls/theme-border-radius.md) control emits ready-made `rounded-*` classes on its own, so it needs no `format` key.
* **Question Size** — a [Theme Text Style](../../component/properties.json/ui-controls/theme-text-style.md) control also emits finished utility classes, combining size and line height from Theme Studio.

The bare `{ "divider": {} }` entries draw separator lines between the controls in the inspector.

### The Behavior Group

Finally, the controls that will drive the accordion logic—two [Switch](../../component/properties.json/ui-controls/switch.md) controls and a [Segmented](../../component/properties.json/ui-controls/segmented.md) control:

```json
{
    "title": "Behavior",
    "icon": "gearshape",
    "properties": [
        {
            "title": "Allow Multiple Open",
            "id": "allowMultipleOpen",
            "responsive": false,
            "switch": { "default": false }
        },
        {
            "title": "First Item Open",
            "id": "firstOpenOnLoad",
            "responsive": false,
            "switch": { "default": true }
        },
        { "divider": {} },
        {
            "title": "Answers",
            "id": "answerType",
            "responsive": false,
            "segmented": {
                "default": "text",
                "items": [
                    { "title": "Text", "value": "text" },
                    { "title": "Dropzone", "value": "dropzone" }
                ]
            }
        }
    ]
}
```

All three are marked `"responsive": false` so they return plain values (a boolean for each switch, the selected `value` string for the segmented control) instead of breakpoint-prefixed classes. That matters because we'll test them with `@if` and JavaScript comparisons later, and only non-responsive values work there.

{% hint style="info" %}
These three controls do nothing yet. The **Answers** mode comes to life in [Part 2](part-2-collections-and-dropzones.md), and the two switches drive the Alpine.js behavior in Part 3. Defining the full inspector now means the later parts only touch `hooks.js` and the templates.
{% endhint %}

## A Minimal hooks.js

The [hooks file](../../component/hooks.js/README.md) runs before every render. The convention used throughout the core pack—see the "Composing Classes in hooks.js" section of [Component Styling](../../component/component-styling.md)—is to gather the formatted class strings from `rw.props`, combine them with static classes in a `classes` object (one string per layer of markup), and hand the result to the template. Our hook does exactly that, in the same plain-array style as the simplified core Button example on that page:

```javascript
// hooks.js
const transformHook = (rw) => {
    const { accentColor, itemGap, itemRadius, questionTextStyle } = rw.props;
    const { id } = rw.node;

    const classes = {
        wrapper: [`group/${id}`, "flex flex-col", itemGap]
            .filter(Boolean)
            .join(" "),
        heading: "font-heading text-2xl text-text-900",
        item: ["overflow-hidden border border-surface-200 bg-surface-50", itemRadius]
            .filter(Boolean)
            .join(" "),
        question: [
            "flex w-full cursor-pointer items-center justify-between gap-4",
            "px-5 py-4 text-left font-semibold",
            questionTextStyle,
            accentColor,
        ]
            .filter(Boolean)
            .join(" "),
        answer: "px-5 pb-5 text-text-700",
    };

    rw.setRootElement({
        as: "div",
        class: classes.wrapper,
    });

    rw.setProps({ classes });
};

exports.transformHook = transformHook;
```

A few things to note:

* Properties like `itemGap` arrive **already formatted**—`gap-y-4`, not `4`—because their controls did the work. The hook just slots them in next to static classes and drops empty entries with `.filter(Boolean)`.
* [`rw.setRootElement()`](../../component/hooks.js/available-functions/rw.setrootelement.md) renders the component as a `<div>` carrying the wrapper classes. `group/${id}` names a Tailwind group after this instance's unique ID—every core component does this so hover and state variants never leak between two copies of the same component on a page.
* [`rw.setProps()`](../../component/hooks.js/available-functions/rw.setprops.md) passes the `classes` object to the template. Untouched properties such as `heading` are available in templates automatically.
* The hooks runtime has no `require` or `import`—everything here is plain JavaScript.

## A Static Template

To prove the styling pipeline works before any real data exists, `templates/index.html` renders two hard-coded questions:

```html
<!-- templates/index.html -->
@if(heading)
<h2 class="{{classes.heading}}">{{heading}}</h2>
@endif

<div class="{{classes.item}}">
    <button type="button" class="{{classes.question}}">
        <span>What is an Element Pack?</span>
        <span aria-hidden="true">+</span>
    </button>
    <div class="{{classes.answer}}">
        A folder-based plugin format for sharing and distributing addons
        for Elements.
    </div>
</div>

<div class="{{classes.item}}">
    <button type="button" class="{{classes.question}}">
        <span>Where does the styling come from?</span>
        <span aria-hidden="true">+</span>
    </button>
    <div class="{{classes.answer}}">
        From the active theme. Formatted controls resolve to Tailwind utility
        classes, so the FAQ follows Theme Studio automatically.
    </div>
</div>
```

The template never sees the full class lists—each layer just references its entry in `{{classes}}`. The `@if(heading)` wrapper hides the `<h2>` entirely when the user clears the heading field, and because the root element is the flex-column wrapper from the hook, the heading and both items pick up the user's Item Gap automatically.

## Try It Out

Drop the FAQ component onto a page. You should see the heading and two permanently-open questions, styled by your theme: brand-colored question text, surface-colored cards with rounded corners, and a gap between items.

_[Screenshot: the FAQ component on the edit canvas showing the heading and two static, open questions]_

Now open the inspector and play with the Style group—switch the accent to another theme color, bump the Item Gap, change the Question Size. Every change re-runs the hook and re-renders with new utility classes, without touching a template.

_[Screenshot: the inspector's Style group next to the canvas, mid-adjustment]_

## Files So Far

The complete component at the end of Part 1—if your files match these, you're ready for Part 2.

#### info.json

```json
{
    "identifier": "com.example.faq",
    "author": "Example Developer",
    "title": "FAQ",
    "group": "Interactive",
    "tags": ["faq", "accordion", "questions"]
}
```

#### properties.json

The three groups from above, combined into one file:

```json
{
    "groups": [
        {
            "title": "Content",
            "icon": "textformat",
            "properties": [
                {
                    "title": "Heading",
                    "id": "heading",
                    "responsive": false,
                    "text": {
                        "default": "Frequently Asked Questions",
                        "placeholder": "Section heading"
                    }
                }
            ]
        },
        {
            "title": "Style",
            "icon": "paintpalette",
            "properties": [
                {
                    "title": "Accent",
                    "id": "accentColor",
                    "format": "text-{{value}}",
                    "themeColor": {
                        "default": { "name": "brand", "brightness": 500 }
                    }
                },
                { "divider": {} },
                {
                    "title": "Item Gap",
                    "id": "itemGap",
                    "format": "gap-y-{{value}}",
                    "themeSpacing": {
                        "mode": "single",
                        "default": { "base": { "value": "4" } }
                    }
                },
                {
                    "title": "Corner Radius",
                    "id": "itemRadius",
                    "themeBorderRadius": {
                        "default": { "base": { "value": "lg" } }
                    }
                },
                { "divider": {} },
                {
                    "title": "Question Size",
                    "id": "questionTextStyle",
                    "themeTextStyle": {
                        "default": { "base": { "name": "lg" } }
                    }
                }
            ]
        },
        {
            "title": "Behavior",
            "icon": "gearshape",
            "properties": [
                {
                    "title": "Allow Multiple Open",
                    "id": "allowMultipleOpen",
                    "responsive": false,
                    "switch": { "default": false }
                },
                {
                    "title": "First Item Open",
                    "id": "firstOpenOnLoad",
                    "responsive": false,
                    "switch": { "default": true }
                },
                { "divider": {} },
                {
                    "title": "Answers",
                    "id": "answerType",
                    "responsive": false,
                    "segmented": {
                        "default": "text",
                        "items": [
                            { "title": "Text", "value": "text" },
                            { "title": "Dropzone", "value": "dropzone" }
                        ]
                    }
                }
            ]
        }
    ]
}
```

#### hooks.js and templates/index.html

Exactly as listed in the "A Minimal hooks.js" and "A Static Template" sections above.

## Next Up

With the scaffolding, inspector, and styling pipeline in place, Part 2 replaces the hard-coded questions with a real collection—and lets individual answers become dropzones:

{% content-ref url="part-2-collections-and-dropzones.md" %}
[part-2-collections-and-dropzones.md](part-2-collections-and-dropzones.md)
{% endcontent-ref %}

## Related Documentation

* [info.json](../../component/info.json.md)
* [Properties](../../component/properties.json/README.md)
* [Grouping Controls](../../component/properties.json/grouping-controls.md)
* [Format](../../component/properties.json/general-structure/format.md)
* [Component Styling](../../component/component-styling.md)
* [Hooks](../../component/hooks.js/README.md)
* [rw.setRootElement](../../component/hooks.js/available-functions/rw.setrootelement.md)
* [rw.setProps](../../component/hooks.js/available-functions/rw.setprops.md)
* [index.html](../../component/templates/index.html.md)
