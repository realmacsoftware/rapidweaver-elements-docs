---
description: Perfect the edit canvas, add dark mode and an advanced escape hatch, emit FAQPage structured data, and ship
---

# Part 4: Edit Mode, Theming & Polish

The FAQ from [Part 3](part-3-interactivity.md) works—but "works" and "ships" are different bars. In this final part you'll fix the published page's first paint without ever hiding an answer on the edit canvas, show placeholder questions while the collection is empty, pair every color for dark mode, add a scoped hover detail and the standard Advanced escape hatch, and emit `FAQPage` structured data so search engines can read the questions too. The part ends with the complete listing of every file in the finished component.

## The Edit Canvas Comes First

A component spends most of its life on the editing canvas, and [Designing the Edit-Mode Experience](../edit-mode-experience.md) sets the bar: every dropzone reachable, no blank boxes, nothing canvas-hostile. Two pieces of work get us there.

### Static First Paint, Always-Open Canvas

Part 3 left a flash: until Alpine boots on the published page, every answer is briefly visible before `x-show` collapses it. The Accordion solves this by rendering the *resting state* statically—its content panel carries `style="display: none;"`, skipped in edit mode so the panel stays open on the canvas. Our version needs one more ingredient, because an answer's resting state depends on three things: it must *never* be hidden on the canvas, and on the published page it should start visible only when it's the first item *and* **First Item Open** is on.

Three inputs is two too many for a template `@if`, which takes exactly [one condition](../../component/language/if.md#combining-conditions). So we follow the rule the edit-mode guide repeats throughout: compute the mode boolean once in `hooks.js` and fold the whole decision into a single per-item flag. The item map from Part 2 gains one line:

```javascript
// hooks.js — per-item resting state (complete file in the final listing below)
const edit = rw.project.mode === "edit";
const firstOpen = isOn(firstOpenOnLoad);

const items = (questions || []).map((item, index) => ({
    ...item,
    index,
    question: item.question || `Question ${index + 1}`,
    questionId: `faq-${id}-question-${index}`,
    answerId: `faq-${id}-answer-${index}`,
    showDropzone: dropzonesEnabled || isOn(item.useDropzone),
    startOpen: edit || (firstOpen && index === 0),
}));
```

`edit` comes from [`rw.project.mode`](../../component/hooks.js/available-data/rw.project.md), exactly as the core Table computes it. On the canvas every item's `startOpen` is `true`; on the published page only the first item's is—and only when the switch says so.

The template consumes the flag as a static seed next to the Alpine bindings, and gives the canvas a truthful `aria-expanded` while it's at it:

```html
<!-- templates/index.html — the per-item changes -->
<button
    type="button"
    id="{{item.questionId}}"
    class="{{classes.question}}"
    @if(edit)
    aria-expanded="true"
    @endif
    :aria-expanded="isOpen({{item.index}}).toString()"
    aria-controls="{{item.answerId}}"
    @click="toggle({{item.index}})"
>
    <span>{{item.question}}</span>
    <span aria-hidden="true" class="{{classes.indicator}}">+</span>
</button>
<div
    id="{{item.answerId}}"
    role="region"
    aria-labelledby="{{item.questionId}}"
    class="{{classes.answer}}"
    x-show="isOpen({{item.index}})"
    x-collapse
    @if(!item.startOpen)
    style="display: none;"
    @endif
>
    @if(item.showDropzone)
    @dropzone("answer", title: "Answer")
    @else
    {{item.answer}}
    @endif
</div>
```

This is the two-mechanism split from the guide's [Keeping Hidden Content Editable](../edit-mode-experience.md#keeping-hidden-content-editable) section: visibility on the canvas is a precomputed inline style (all answers open, every dropzone reachable), visibility at runtime belongs to Alpine, and after boot the factory's `x-show` takes ownership of the attribute the seed put there. First paint now matches the resting state in every combination—no flash with **First Item Open** on or off. (The `{{classes.indicator}}` span is new too; it's wired up in the theming section below.)

### Placeholder Questions for an Empty Collection

Delete every question and Part 3's FAQ renders only a heading—a blank box with extra steps. The fix is the same fallback trick the core Audio Playlist uses for its missing first track (see the [full example in Data Collections in hooks.js](../../component/collections/data-collections-in-hooks.js.md#full-example-audio-playlist)): when the collection is empty, substitute a hard-coded sample array so the component still renders its real layout.

```javascript
// hooks.js — placeholder questions (complete file in the final listing below)
const placeholderQuestions = [
    {
        question: "What kinds of questions belong here?",
        answer: "Short, factual ones. Add your first question in the inspector and these placeholders disappear.",
    },
    {
        question: "Can an answer hold other components?",
        answer: "Yes. Flip Use Dropzone on any question, or switch every answer to Dropzone in the Behavior group.",
    },
];

const usingPlaceholders = !questions || questions.length === 0;
const sourceItems = usingPlaceholders ? placeholderQuestions : questions;

const showPlaceholderHint = edit && usingPlaceholders;
```

The item map from the previous section now runs over `sourceItems` instead of `(questions || [])`, so placeholders flow through the same ID, ARIA, and `startOpen` enrichment as real questions. Like the Gallery's empty state, the placeholder is [keyed to content, not mode](../edit-mode-experience.md#empty-state-placeholders)—an empty FAQ previews as a working accordion, not a void. The dimmed caption explaining the situation, though, is editor guidance, and "in edit mode *and* using placeholders" is another two-input decision—hence the precomputed `showPlaceholderHint`. The template appends it after the list wrapper:

```html
<!-- templates/index.html — after the closing </div> of the list wrapper -->
@if(showPlaceholderHint)
<p class="text-sm text-text-500 dark:text-text-400">
    Example questions&mdash;add your own in the inspector's Questions panel
    and these disappear.
</p>
@endif
```

## Theming Polish

Three refinements finish the styling story. Here is the hook's finished `classes` object with every change from this part—the subsections walk through the additions:

```javascript
// hooks.js — the finished classes object
const classes = {
    wrapper: [`group/${id}`, "flex flex-col", itemGap, cssClasses]
        .filter(Boolean)
        .join(" "),
    heading: "font-heading text-2xl text-text-900 dark:text-text-100",
    list: ["flex flex-col", itemGap].filter(Boolean).join(" "),
    item: [
        `group/item-${id}`,
        "overflow-hidden border border-surface-200 bg-surface-50",
        "dark:border-surface-700 dark:bg-surface-900",
        itemRadius,
    ]
        .filter(Boolean)
        .join(" "),
    question: [
        "flex w-full cursor-pointer items-center justify-between gap-4",
        "px-5 py-4 text-left font-semibold",
        "hover:bg-surface-100 dark:hover:bg-surface-800",
        questionTextStyle,
        accentColor,
    ]
        .filter(Boolean)
        .join(" "),
    answer: "px-5 pb-5 text-text-700 dark:text-text-300",
    indicator: [
        "inline-block transition-transform duration-200",
        `group-hover/item-${id}:scale-125`,
    ].join(" "),
};
```

### Dark-Mode Color Pairing

Every hard-coded color now travels with a `dark:` partner—light surfaces pair with dark ones (`bg-surface-50` / `dark:bg-surface-900`), dark text pairs with light (`text-text-900` / `dark:text-text-100`), and the hover tint pairs too. This is the pairing convention described in the [Dark Mode](../../component/component-styling.md#dark-mode) section of Component Styling; if you ever stack another variant on top of a paired value, remember that the new prefix must land *after* `dark:`—that section covers the rewrite (and the Build Tools helper that automates it).

The **Accent** control gets its dark half declaratively instead: a [Theme Color](../../component/properties.json/ui-controls/theme-color.md#setting-light-and-dark-mode-colours) control with `darkName`/`darkBrightness` emits a ready-made pair, which our `format` turns into `text-brand-500 dark:text-brand-400`. One edit in `properties.json`:

```json
{
    "title": "Accent",
    "id": "accentColor",
    "format": "text-{{value}}",
    "themeColor": {
        "default": {
            "name": "brand",
            "brightness": 500,
            "darkName": "brand",
            "darkBrightness": 400
        }
    }
}
```

### A Scoped Hover Group per Item

The `+` indicator should react when the pointer is anywhere over its item—a different element than the one being hovered, which is exactly what Tailwind's [named groups](../../component/component-styling.md#named-groups-for-scoped-hover-states) are for. The wrapper's `group/${id}` from Part 1 is the wrong tool here: `group-hover` compiles to a *descendant* selector, so a group on the wrapper would fire every item's indicator whenever the pointer touched any part of the FAQ. Instead each item carries its own named group, `group/item-${id}`, and the indicator opts in with `group-hover/item-${id}:scale-125`.

Keeping the instance ID in the item's group name matters for the same reason it does on the wrapper: dropzone answers mean one FAQ can legitimately sit inside another, and an unscoped `group/item` on the outer item would scale the *inner* FAQ's indicators—they'd be descendants with a matching group name. Keyed to the ID, hover states never leak between instances. (The question's background tint needs no group at all—the hovered element and the styled element are the same, so a plain `hover:` variant does it.)

### The Advanced Escape Hatch

Every core component ends its inspector with an Advanced group whose **Classes** field lets power users append their own utility classes—the convention documented in [Supporting User-Defined Classes](../../component/component-styling.md#supporting-user-defined-classes). We adopt the same control shape (a text area with the id `cssClasses`, matching the core components) as a fourth group in `properties.json`:

```json
{
    "title": "Advanced",
    "icon": "wrench.and.screwdriver",
    "properties": [
        {
            "title": "Classes",
            "id": "cssClasses",
            "textArea": { "default": "" }
        }
    ]
}
```

The hook destructures `cssClasses` from `rw.props` and appends it as the last entry of the wrapper's class array (see the finished `classes` object above)—`.filter(Boolean)` already drops it when empty.

## FAQPage Structured Data

An FAQ is one of the few components whose content search engines understand natively: mark it up as [`FAQPage`](https://schema.org/FAQPage) JSON-LD and the questions become machine-readable. The data is assembled in the hook, where the real strings live, with `JSON.stringify` doing the serialising:

```javascript
// hooks.js — structured data (complete file in the final listing below)
const textFaqs = usingPlaceholders
    ? []
    : items.filter((item) => !item.showDropzone && item.answer);

const jsonLd = JSON.stringify({
    "@context": "https://schema.org",
    "@type": "FAQPage",
    "mainEntity": textFaqs.map((item) => ({
        "@type": "Question",
        "name": item.question,
        "acceptedAnswer": {
            "@type": "Answer",
            "text": item.answer,
        },
    })),
});
```

Two kinds of item are deliberately excluded:

* **Placeholder questions.** Structured data describing sample content would be lying to search engines, so `usingPlaceholders` empties the list outright.
* **Dropzone answers.** The hook sees an item's *data*—its `answer` text—but a dropzone's contents are other components whose rendered output the hook can never read as a string. Structured data must mirror what's visibly on the page, so any item with `showDropzone` (or an empty answer) is simply not listed. The rest of the FAQ still qualifies.

The template emits the block into the page head through a portal—add this at the very top of `templates/index.html`:

```html
<!-- templates/index.html — added at the very top of the file -->
@if(hasJsonLd)
@portal(headEnd)
<script type="application/ld+json">
{{jsonLd}}
</script>
@endportal
@endif
```

Note what's *missing* compared to `templates/alpine.html`: no `includeOnce`, no `id`. That's deliberate. The Alpine factory is shared, identical logic—include it once. This block is **per-instance data**: two FAQ components on one page should emit two `FAQPage` blocks, each describing its own questions, which is perfectly valid structured data. An `includeOnce` portal would keep only the first instance's block and silently drop the rest—the exact failure mode the [portals warning](../interactive-components-with-alpine.md#shipping-styles-through-portals) in the Alpine guide describes. `hasJsonLd` (set to `textFaqs.length > 0` in the hook) keeps empty `mainEntity` arrays out of the head entirely.

{% hint style="warning" %}
`JSON.stringify` is the escaping story: it handles quotes, backslashes, and control characters in whatever users type, so never assemble the JSON by string concatenation. And keep the Answer field plain text—raw HTML pasted into it would be carried verbatim into the script block, and structured-data answer text shouldn't contain markup your page doesn't visibly render.
{% endhint %}

## Try It Out

Give the finished component a shakedown. Delete every question and watch the placeholders and their editor-only caption appear; add a question back and they vanish. Switch your theme (or system appearance) to dark and check the surfaces, text, and accent all flip. Hover an item and watch the indicator grow. Then publish and view source: one `application/ld+json` block per FAQ in the `<head>`, listing exactly the text answers.

_[Screenshot: the empty-collection FAQ on the canvas showing two placeholder questions and the dimmed caption]_

_[Screenshot: the published FAQ in dark mode, one item hovered with its indicator enlarged]_

## The Finished Component

Every file of `com.example.faq`, complete. This is the final state of everything built across all four parts.

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

```json
{
    "groups": [
        {
            "title": "Content",
            "icon": "textformat",
            "properties": [
                {
                    "title": "Questions",
                    "id": "questions",
                    "collection": {
                        "identifier": "com.example.faq.collections.questions"
                    }
                },
                { "divider": {} },
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
                        "default": {
                            "name": "brand",
                            "brightness": 500,
                            "darkName": "brand",
                            "darkBrightness": 400
                        }
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
        },
        {
            "title": "Advanced",
            "icon": "wrench.and.screwdriver",
            "properties": [
                {
                    "title": "Classes",
                    "id": "cssClasses",
                    "textArea": { "default": "" }
                }
            ]
        }
    ]
}
```

#### collections/questions/info.json

```json
{
    "identifier": "com.example.faq.collections.questions",
    "title": "Questions"
}
```

#### collections/questions/properties.json

```json
{
    "groups": [
        {
            "title": "Question",
            "properties": [
                {
                    "title": "Question",
                    "property": "question",
                    "responsive": false,
                    "text": { "default": "" }
                },
                {
                    "title": "Answer",
                    "property": "answer",
                    "responsive": false,
                    "textArea": { "size": 4, "default": "" }
                },
                { "divider": {} },
                {
                    "title": "Use Dropzone",
                    "property": "useDropzone",
                    "responsive": false,
                    "switch": { "default": false }
                }
            ]
        }
    ]
}
```

#### collections/questions/defaults.json

```json
{
    "items": [
        {
            "question": "What does shipping cost?",
            "answer": "Standard shipping is free on orders over $50. Express options are calculated at checkout."
        },
        {
            "question": "Can I change my order after placing it?",
            "answer": "Orders can be edited for up to one hour after checkout. After that, contact support and we'll do our best to help."
        },
        {
            "question": "Do you offer refunds?",
            "answer": "Every plan comes with a 30-day money-back guarantee, no questions asked."
        }
    ]
}
```

#### hooks.js

```javascript
// hooks.js
const transformHook = (rw) => {
    const {
        accentColor,
        itemGap,
        itemRadius,
        questionTextStyle,
        answerType,
        allowMultipleOpen,
        firstOpenOnLoad,
        cssClasses,
    } = rw.props;
    const { id } = rw.node;
    const { questions } = rw.collections;

    const isOn = (value) => value === true || value === "true";
    const edit = rw.project.mode === "edit";

    const dropzonesEnabled = answerType === "dropzone";
    const firstOpen = isOn(firstOpenOnLoad);

    const placeholderQuestions = [
        {
            question: "What kinds of questions belong here?",
            answer: "Short, factual ones. Add your first question in the inspector and these placeholders disappear.",
        },
        {
            question: "Can an answer hold other components?",
            answer: "Yes. Flip Use Dropzone on any question, or switch every answer to Dropzone in the Behavior group.",
        },
    ];

    const usingPlaceholders = !questions || questions.length === 0;
    const sourceItems = usingPlaceholders ? placeholderQuestions : questions;

    const items = sourceItems.map((item, index) => ({
        ...item,
        index,
        question: item.question || `Question ${index + 1}`,
        questionId: `faq-${id}-question-${index}`,
        answerId: `faq-${id}-answer-${index}`,
        showDropzone: dropzonesEnabled || isOn(item.useDropzone),
        startOpen: edit || (firstOpen && index === 0),
    }));

    const faqConfigJson = JSON.stringify({
        allowMultipleOpen: isOn(allowMultipleOpen),
        firstOpenOnLoad: firstOpen,
    });

    const textFaqs = usingPlaceholders
        ? []
        : items.filter((item) => !item.showDropzone && item.answer);

    const jsonLd = JSON.stringify({
        "@context": "https://schema.org",
        "@type": "FAQPage",
        "mainEntity": textFaqs.map((item) => ({
            "@type": "Question",
            "name": item.question,
            "acceptedAnswer": {
                "@type": "Answer",
                "text": item.answer,
            },
        })),
    });

    const classes = {
        wrapper: [`group/${id}`, "flex flex-col", itemGap, cssClasses]
            .filter(Boolean)
            .join(" "),
        heading: "font-heading text-2xl text-text-900 dark:text-text-100",
        list: ["flex flex-col", itemGap].filter(Boolean).join(" "),
        item: [
            `group/item-${id}`,
            "overflow-hidden border border-surface-200 bg-surface-50",
            "dark:border-surface-700 dark:bg-surface-900",
            itemRadius,
        ]
            .filter(Boolean)
            .join(" "),
        question: [
            "flex w-full cursor-pointer items-center justify-between gap-4",
            "px-5 py-4 text-left font-semibold",
            "hover:bg-surface-100 dark:hover:bg-surface-800",
            questionTextStyle,
            accentColor,
        ]
            .filter(Boolean)
            .join(" "),
        answer: "px-5 pb-5 text-text-700 dark:text-text-300",
        indicator: [
            "inline-block transition-transform duration-200",
            `group-hover/item-${id}:scale-125`,
        ].join(" "),
    };

    rw.setRootElement({
        as: "div",
        class: classes.wrapper,
    });

    rw.setProps({
        id,
        classes,
        questions: items,
        faqConfigJson,
        showPlaceholderHint: edit && usingPlaceholders,
        hasJsonLd: textFaqs.length > 0,
        jsonLd,
    });
};

exports.transformHook = transformHook;
```

#### templates/index.html

```html
<!-- templates/index.html -->
@if(hasJsonLd)
@portal(headEnd)
<script type="application/ld+json">
{{jsonLd}}
</script>
@endportal
@endif

@if(heading)
<h2 class="{{classes.heading}}">{{heading}}</h2>
@endif

<div
    x-data="exampleFaq('{{id}}')"
    x-bind="list"
    data-faq-config='{{faqConfigJson}}'
    class="{{classes.list}}"
>
    @each(item in questions)
    <div class="{{classes.item}}">
        <button
            type="button"
            id="{{item.questionId}}"
            class="{{classes.question}}"
            @if(edit)
            aria-expanded="true"
            @endif
            :aria-expanded="isOpen({{item.index}}).toString()"
            aria-controls="{{item.answerId}}"
            @click="toggle({{item.index}})"
        >
            <span>{{item.question}}</span>
            <span aria-hidden="true" class="{{classes.indicator}}">+</span>
        </button>
        <div
            id="{{item.answerId}}"
            role="region"
            aria-labelledby="{{item.questionId}}"
            class="{{classes.answer}}"
            x-show="isOpen({{item.index}})"
            x-collapse
            @if(!item.startOpen)
            style="display: none;"
            @endif
        >
            @if(item.showDropzone)
            @dropzone("answer", title: "Answer")
            @else
            {{item.answer}}
            @endif
        </div>
    </div>
    @endeach
</div>

@if(showPlaceholderHint)
<p class="text-sm text-text-500 dark:text-text-400">
    Example questions&mdash;add your own in the inspector's Questions panel
    and these disappear.
</p>
@endif
```

#### templates/alpine.html

```html
<!-- templates/alpine.html -->
@portal(bodyEnd, includeOnce: true, id: "com.example.faq.alpine")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("exampleFaq", (id) => ({
            id,
            open: [],
            config: { allowMultipleOpen: false, firstOpenOnLoad: true },

            init() {
                try {
                    Object.assign(
                        this.config,
                        JSON.parse(this.$el.dataset.faqConfig || "{}")
                    );
                } catch (e) {
                    console.warn("FAQ " + this.id + ": invalid config JSON");
                }
                if (this.config.firstOpenOnLoad) {
                    this.open = [0];
                }
            },

            isOpen(index) {
                return this.open.includes(index);
            },

            toggle(index) {
                if (this.isOpen(index)) {
                    this.open = this.open.filter((i) => i !== index);
                    return;
                }
                this.open = [...this.open, index];
                if (!this.config.allowMultipleOpen) {
                    this.$dispatch("close-faq-answers", {
                        id: this.id,
                        except: index,
                    });
                }
            },

            list: {
                ["@close-faq-answers.window"](event) {
                    const { id, except } = event.detail;
                    if (id !== this.id) {
                        return;
                    }
                    this.open = this.open.filter((i) => i === except);
                },
            },
        }));
    });
</script>
@endportal
```

## Before You Ship

{% hint style="success" %}
**Ship checklist** — run through this before releasing the FAQ:

* [ ] The canvas shows every answer open and every dropzone reachable, with any items added, removed, or reordered.
* [ ] An empty collection renders the placeholder questions—never a blank box—and the caption appears only on the canvas.
* [ ] Every template `@if` tests a single condition; anything combining mode, switches, or indices is precomputed in `hooks.js`.
* [ ] The published first paint matches the resting state with **First Item Open** both on and off—no flash of open or closed content.
* [ ] Two FAQ instances on one page open and close independently, including with **Allow Multiple Open** set differently on each.
* [ ] Keyboard: Tab reaches each question button, Enter/Space toggles it, and `aria-expanded` follows the state.
* [ ] Dark mode: every hard-coded color has a `dark:` partner, and the Accent control's dark value renders.
* [ ] The JSON-LD block validates in a structured-data testing tool, lists only text answers, and is absent while placeholders show.
{% endhint %}

## Where to Go Next

The FAQ touches most of the component surface area, but each topic goes deeper than one tutorial can:

{% content-ref url="../interactive-components-with-alpine.md" %}
[interactive-components-with-alpine.md](../interactive-components-with-alpine.md)
{% endcontent-ref %}

Full lifecycles (`init()`/`destroy()`), reduced-motion handling, and the Tabs keyboard pattern—arrow keys and a roving tabindex would be a natural upgrade for this FAQ's question buttons.

{% content-ref url="../modals-overlays-and-portals.md" %}
[modals-overlays-and-portals.md](../modals-overlays-and-portals.md)
{% endcontent-ref %}

Portals as a layout tool: moving overlay markup to `bodyEnd` and wiring open/close triggers across components.

{% content-ref url="../integrating-javascript-libraries.md" %}
[integrating-javascript-libraries.md](../integrating-javascript-libraries.md)
{% endcontent-ref %}

When Alpine isn't enough: bundling third-party libraries into a pack and driving them from properties.

## Related Documentation

* [Designing the Edit-Mode Experience](../edit-mode-experience.md)
* [Component Styling](../../component/component-styling.md)
* [Data Collections in hooks.js](../../component/collections/data-collections-in-hooks.js.md)
* [Theme Color](../../component/properties.json/ui-controls/theme-color.md)
* [rw.project](../../component/hooks.js/available-data/rw.project.md)
* [@portal](../../component/language/portal.md)
* [@if](../../component/language/if.md)
* [Interactive Components with Alpine.js](../interactive-components-with-alpine.md)
