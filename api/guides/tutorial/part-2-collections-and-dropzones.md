---
description: Drive the FAQ from a questions collection and let individual answers become dropzones
---

# Part 2: Collections & Dynamic Dropzones

At the end of [Part 1](part-1-scaffolding-and-properties.md) the FAQ renders two hard-coded questions. In this part the questions become real data: a `questions` [collection](../../component/collections/README.md) that users manage in the inspector, a hook that enriches each item with IDs, ARIA attributes, and precomputed booleans, and a template loop where each answer is either plain text or a dropzone. This is the same architecture the core Tabs and Table components use for their repeating content.

## Define the Questions Collection

Collections live in a `collections/` folder at the root of the component, one subfolder per collection. Create the folder and its three files:

```
com.example.faq/
├── collections/
│   └── questions/
│       ├── info.json
│       ├── properties.json
│       └── defaults.json
├── ...
```

### collections/questions/info.json

The collection's own manifest identifies it to Elements. The convention—documented in [Collections](../../component/collections/README.md) and followed by every core component—is to extend the component identifier with `.collections.{name}`:

```json
{
    "identifier": "com.example.faq.collections.questions",
    "title": "Questions"
}
```

`title` is the label shown above the collection panel in the inspector.

### collections/questions/properties.json

This file describes the fields of **each item** in the collection, using the same control vocabulary as component properties. Three fields per question: the question itself, a text answer, and a per-item switch to swap that answer for a dropzone:

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

Walking through it against the [collections reference](../../component/collections/README.md):

* Item fields use the key `property` where component controls use `id`—compare this file with the component-level `properties.json` from Part 1. The core Tabs and Table collections are written exactly this way.
* `question` is a [Text](../../component/properties.json/ui-controls/text.md) control and `answer` is a [Text Area](../../component/properties.json/ui-controls/text-area.md) (`size` sets its height in rows)—answers are usually a sentence or three.
* `useDropzone` is a per-item [Switch](../../component/properties.json/ui-controls/switch.md). The core Table has the same idea on its columns collection (a per-column "Cell Mode" choice between text and dropzone).
* Everything is `"responsive": false`—collection fields are data, not styling, so breakpoint variants make no sense here.

### collections/questions/defaults.json

Without defaults, a freshly dropped FAQ would be empty. `defaults.json` pre-populates the collection so users see the component working immediately:

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

Each object supplies values for the `property` names defined above; anything omitted (like `useDropzone`) falls back to the field's own default.

## Register the Collection in properties.json

The collection folder alone does nothing—the component's main `properties.json` must reference it with a `collection` control, as described in [Collections in properties.json](../../component/collections/collections-in-properties.json.md). Replace Part 1's Content group with this—the Style and Behavior groups stay unchanged:

```json
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
}
```

The `collection.identifier` must match `collections/questions/info.json` exactly, and the `id` becomes the property name the data is exposed under: `rw.collections.questions` in hooks and `collections.questions` in templates. This registration is shaped just like the core Tabs component's, which registers its collection as `{ "title": "Tabs", "id": "tabs", "collection": { "identifier": "com.realmacsoftware.tabs.collections.tabs" } }` at the top of its Settings group.

Save, and the inspector's Content group now shows a Questions panel where items can be added, edited, reordered, and removed.

_[Screenshot: the inspector's Content group with the Questions collection panel showing the three default items]_

## Prepare Items in hooks.js

We could loop over `collections.questions` directly in the template, but the core components almost never do—they enrich each item in the hook first, then pass the processed array to the template. Two reasons apply here:

**1. Accessibility needs stable IDs.** Each question button should carry `aria-expanded` and point at its answer region via `aria-controls`; the answer points back with `aria-labelledby`. That requires a unique pair of element IDs per item. The core Tabs hook builds them by combining the component instance's ID with the item index:

```javascript
// com.realmacsoftware.tabs — hooks.source.js (excerpt)
const tabItems = tabs?.map((tab, index) => {
    // …
    return {
        id: `tab-${id}-${index}`,
        title: tab.title || `Tab ${index + 1}`,
        // …
    };
}) || [];
```

**2. Template `@if` takes exactly one condition.** No `&&`, `||`, or comparisons are allowed inside `@if(...)`—see [Combining Conditions](../../component/language/if.md#combining-conditions). Whether an item's answer is a dropzone depends on *two* values: the component-level **Answers** segmented control and the item's own **Use Dropzone** switch. So we combine them in the hook into a single `showDropzone` boolean per item, and the template tests only that.

Here are the additions—the `classes` object and the `rw.setRootElement()` call are unchanged from Part 1, and the complete file is in the checkpoint at the end of this page:

```javascript
// hooks.js — the additions (complete file in the checkpoint below)
const { questions } = rw.collections;

// Switch values can surface as booleans or strings depending on context,
// so normalise them once. The core Table and Tabs hooks do the same.
const isOn = (value) => value === true || value === "true";

const dropzonesEnabled = answerType === "dropzone";

const items = (questions || []).map((item, index) => ({
    ...item,
    index,
    question: item.question || `Question ${index + 1}`,
    questionId: `faq-${id}-question-${index}`,
    answerId: `faq-${id}-answer-${index}`,
    showDropzone: dropzonesEnabled || isOn(item.useDropzone),
}));
```

The hook also destructures `answerType` from `rw.props` alongside the style properties, and its final `rw.setProps()` call now passes the processed array: `rw.setProps({ classes, questions: items })`.

The interesting decisions:

* `rw.collections.questions` is the raw item array ([rw.collections](../../component/hooks.js/available-data/rw.collections.md)); the guard `(questions || [])` keeps the hook safe when the collection is empty.
* Each processed item keeps its original fields (`...item`) and gains `index`, a fallback `question` label, the two element IDs, and `showDropzone`.
* `showDropzone` is true when the component-wide **Answers** control is set to Dropzone *or* the item's own **Use Dropzone** switch is on—so Text mode is the default, individual items can opt in, and flipping the segmented control converts every answer at once.
* The processed array is passed to the template as `questions` via [rw.setProps](../../component/hooks.js/available-functions/rw.setprops.md). The raw data remains available as `collections.questions`, but the template only uses the enriched version—the same convention as the core Audio Playlist and Tabs templates.

## Render the Loop in index.html

Replace the two hard-coded items with an [@each](../../component/language/each.md) loop. The `@if(heading)` block from Part 1 stays as it is; everything below it becomes this:

```html
<!-- templates/index.html — the loop that replaces the two static items -->
@each(item in questions)
<div class="{{classes.item}}">
    <button
        type="button"
        id="{{item.questionId}}"
        class="{{classes.question}}"
        aria-expanded="true"
        aria-controls="{{item.answerId}}"
    >
        <span>{{item.question}}</span>
        <span aria-hidden="true">+</span>
    </button>
    <div
        id="{{item.answerId}}"
        role="region"
        aria-labelledby="{{item.questionId}}"
        class="{{classes.answer}}"
    >
        @if(item.showDropzone)
        @dropzone("answer", title: "Answer")
        @else
        {{item.answer}}
        @endif
    </div>
</div>
@endeach
```

Two things deserve a closer look.

### The Dropzone-or-Text Answer

The `@if(item.showDropzone)` branch is the payoff of the hook work: one precomputed boolean chooses between rendering the item's `answer` text and emitting an [@dropzone](../../component/language/dropzone.md). This pattern comes straight from the core Table component, whose body cells do exactly the same per-column switch:

```html
<!-- com.realmacsoftware.table — templates/index.php (excerpt) -->
@if(column.isDropzone)
    @dropzone("cell", title: "Cell")
@else
    @text("cell", default: "Cell")
@endif
```

(The Table renders an inline-editable `@text` in its else branch; our FAQ prints the collection field instead.) For a deeper look at how collections and dropzones interact, see [Collection-Driven Dropzones](../collection-driven-dropzones.md).

Note that the dropzone's name is the static literal `"answer"` even though it sits inside a loop—dropzone names can't contain template variables. Elements automatically creates a unique dropzone per iteration and keeps its contents attached to the right item, even when items are reordered. See [Dropzones Inside Loops](../../component/language/dropzone.md#dropzones-inside-loops).

### ARIA Now, Interactivity Next

The button hard-codes `aria-expanded="true"` because every answer really is visible right now—there is no open/close state yet. The IDs wired through `aria-controls` and `aria-labelledby` are the piece worth doing early: they're pure data, so they belong in the hook, and Part 3 will simply rebind `aria-expanded` (and hide closed answers) with Alpine without touching the IDs again.

## Try It Out

Add and reorder questions in the inspector and watch the accordion follow. Then exercise the dropzone logic:

1. Open one item and flip **Use Dropzone** on—its text answer is replaced by an empty dropzone. Drop an Image or List component in.
2. Switch the Behavior group's **Answers** control to **Dropzone**—every answer becomes a dropzone, regardless of the per-item switches.

_[Screenshot: the FAQ on the canvas with two text answers and one dropzone answer containing an Image component]_

If you delete every question the component renders only the heading—Part 4 adds placeholder items for that case, so don't worry about it yet.

## Checkpoint: Full Files So Far

At the end of Part 2, `info.json` is unchanged from Part 1, `properties.json` differs only by the Content group shown above, and the three collection files are listed in full earlier on this page. The two files that changed substantially are worth checking end to end—Part 3 starts from exactly these.

#### hooks.js

The complete file—Part 1's hook plus the item preparation:

```javascript
// hooks.js
const transformHook = (rw) => {
    const { accentColor, itemGap, itemRadius, questionTextStyle, answerType } =
        rw.props;
    const { id } = rw.node;
    const { questions } = rw.collections;

    const isOn = (value) => value === true || value === "true";

    const dropzonesEnabled = answerType === "dropzone";

    const items = (questions || []).map((item, index) => ({
        ...item,
        index,
        question: item.question || `Question ${index + 1}`,
        questionId: `faq-${id}-question-${index}`,
        answerId: `faq-${id}-answer-${index}`,
        showDropzone: dropzonesEnabled || isOn(item.useDropzone),
    }));

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

    rw.setProps({
        classes,
        questions: items,
    });
};

exports.transformHook = transformHook;
```

#### templates/index.html

The complete file—the heading from Part 1 followed by the loop:

```html
<!-- templates/index.html -->
@if(heading)
<h2 class="{{classes.heading}}">{{heading}}</h2>
@endif

@each(item in questions)
<div class="{{classes.item}}">
    <button
        type="button"
        id="{{item.questionId}}"
        class="{{classes.question}}"
        aria-expanded="true"
        aria-controls="{{item.answerId}}"
    >
        <span>{{item.question}}</span>
        <span aria-hidden="true">+</span>
    </button>
    <div
        id="{{item.answerId}}"
        role="region"
        aria-labelledby="{{item.questionId}}"
        class="{{classes.answer}}"
    >
        @if(item.showDropzone)
        @dropzone("answer", title: "Answer")
        @else
        {{item.answer}}
        @endif
    </div>
</div>
@endeach
```

## Next Up

The FAQ now has real data, accessible markup, and flexible answers—but every answer is permanently open. Part 3 brings the accordion to life with Alpine.js:

{% content-ref url="part-3-interactivity.md" %}
[part-3-interactivity.md](part-3-interactivity.md)
{% endcontent-ref %}

## Related Documentation

* [Collections](../../component/collections/README.md)
* [Collections in properties.json](../../component/collections/collections-in-properties.json.md)
* [Data Collections in hooks.js](../../component/collections/data-collections-in-hooks.js.md)
* [Accessing Data in Templates](../../component/collections/accessing-data-in-templates.md)
* [rw.collections](../../component/hooks.js/available-data/rw.collections.md)
* [@each](../../component/language/each.md)
* [@if](../../component/language/if.md)
* [@dropzone](../../component/language/dropzone.md)
