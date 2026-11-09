---
description: Bring the accordion to life with an Alpine.js factory, one-open-at-a-time state, and collapse transitions
---

# Part 3: Interactivity with Alpine.js

At the end of [Part 2](part-2-collections-and-dropzones.md) the FAQ renders real questions with accessible markup—but every answer sits permanently open. In this part you'll add the accordion behavior: an Alpine.js **factory** registered once per page in a new `templates/alpine.html`, per-instance configuration passed through a `data-*` attribute, open/close state that honors the **First Item Open** and **Allow Multiple Open** switches, and smooth `x-collapse` transitions. The architecture is a scaled-down version of the core Accordion's, and the reasoning behind every piece is covered in depth in [Interactive Components with Alpine.js](../interactive-components-with-alpine.md)—this part applies the pattern rather than re-explaining it.

## Nothing to Install

Alpine and the plugins the core components rely on are already on every Elements page: the Core Pack's shared setup template loads Alpine v3 along with `alpine-collapse.js`—the plugin that provides the `x-collapse` directive—from its `shared/assets/` folder, with each plugin listed before `alpine.js` so registration order takes care of itself. The [Why Alpine.js](../interactive-components-with-alpine.md#why-alpinejs) section of the Alpine guide shows the exact script list. For our FAQ this means there is no library to bundle and no `<script src>` to write—we only register our own factory and use the directives.

## The Factory in templates/alpine.html

The naive approach—a `<script>` block in `index.html`—would be emitted once per FAQ on the page. Instead, the core convention is a separate template, conventionally named `alpine.html`, whose entire contents sit inside a deduplicated portal. Every root-level file in `templates/` is [processed automatically for each instance](../../component/templates/README.md#root-level-templates), so the file needs no `@include` from `index.html`—the portal's `includeOnce` guarantees the script lands exactly once no matter how many FAQs exist. (Some core components, like Tabs, add `@include("alpine")` at the top of `index.html` anyway; it's harmless for the same reason.)

Create `templates/alpine.html` with the skeleton every core factory shares—compare it with the Accordion's `templates/alpine.html`, which opens identically:

```html
<!-- templates/alpine.html — the wrapper -->
@portal(bodyEnd, includeOnce: true, id: "com.example.faq.alpine")
<script>
    document.addEventListener("alpine:init", () => {
        // Alpine.data("exampleFaq", …) goes here
    });
</script>
@endportal
```

All three wrapper details are load-bearing: `bodyEnd` moves the script to the end of `<body>`, `includeOnce` with a reverse-DNS `id` deduplicates it across instances, and the `alpine:init` listener registers the factory before Alpine parses the page's `x-data` attributes. The [Factory Pattern](../interactive-components-with-alpine.md#the-factory-pattern) section explains what goes wrong when any of the three is skipped.

### State: Which Items Are Open

Inside the listener, register the factory. Its state is a single array, `open`, holding the indices of the currently expanded items—an array rather than a single value because **Allow Multiple Open** legitimately allows several at once:

```javascript
// templates/alpine.html — the factory's state and init()
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
    // … isOpen, toggle, and the list binding group — next section …
}));
```

`init()` runs once per instance. It reads the configuration from a `data-faq-config` attribute on the element that carries `x-data` (written in the next section), merges it over sensible defaults so a malformed attribute can't crash the component, and—if **First Item Open** is on—starts with item `0` expanded.

### One Open at a Time: the Accordion's Group-Close Mechanic

Toggling is where the two Behavior switches meet. Opening an item always adds its index; what happens to the *other* open items is decided by an event, not by the toggle itself:

```javascript
// templates/alpine.html — toggling (the rest of the factory object)
Alpine.data("exampleFaq", (id) => ({
    // … state and init() from above …

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
```

This is the core Accordion's group-close mechanic, transplanted: when something opens, `$dispatch` broadcasts a custom event to `window`, and a window-level listener enforces the "only one open" rule by closing everything else. The Accordion uses it to coordinate *separate component instances* in a group—each one listens, compares the payload's `groupId` against its own, and closes itself if it's a sibling but **not** the sender. Our FAQ holds all of its items inside *one* instance, so the check is the mirror image: the listener acts only when the event's `id` **matches** its own, keeping two FAQ components on the same page from closing each other's answers. The full round trip—`$watch`, `$dispatch`, the `.window` modifier, and why no instance ever holds a reference to another—is dissected in [The Factory Pattern](../interactive-components-with-alpine.md#the-factory-pattern).

Could `toggle` just do `this.open = [index]` and skip the event? Yes—but the event buys two things. The close rule lives in exactly one listener, so any future way of opening an item (a hash-fragment deep link, an "expand all" button) respects it automatically. And it keeps our code shaped like the Accordion's, so everything the Alpine guide says about that component maps onto this one line for line. The `list` object, incidentally, is a [binding group](../interactive-components-with-alpine.md#organizing-state-with-binding-groups)—a bag of Alpine directives applied wholesale with `x-bind="list"`.

Notice that state changes always *reassign* `open` (`filter`, spread) rather than mutating it in place—each assignment is one unambiguous reactive update for Alpine to propagate.

## Passing the Configuration

The factory expects its options in a `data-faq-config` attribute, so the hook's job is to serialise the two Behavior switches to JSON. Add the two properties to the destructuring, then build the string—the `isOn` helper from Part 2 normalises the switch values first:

```javascript
// hooks.js — the additions (complete file in the checkpoint below)
const { allowMultipleOpen, firstOpenOnLoad } = rw.props;

const faqConfigJson = JSON.stringify({
    allowMultipleOpen: isOn(allowMultipleOpen),
    firstOpenOnLoad: isOn(firstOpenOnLoad),
});
```

The hook's final `rw.setProps()` call passes two new values alongside the existing ones—`faqConfigJson`, and the instance `id` (from `rw.node`) that the template will interpolate into `x-data`:

```javascript
rw.setProps({
    id,
    classes,
    questions: items,
    faqConfigJson,
});
```

{% hint style="info" %}
Serialising with `JSON.stringify` in `hooks.js` and embedding the result in a **single-quoted `data-*` attribute** is the recommended way to hand structured configuration to a factory: the single quotes keep JSON's double-quotes intact, and `JSON.parse` in `init()` gets the object back untouched—the core Image component passes its lightbox breakpoints exactly this way. The alternative is the *quote-swap* pattern (`JSON.stringify(…).replace(/"/g, "'")`) used by the Accordion and Content Slider, which is fine for config you fully control but corrupts data containing quote characters. Both patterns, with failure modes, are covered in [JavaScript Templates](../../component/templates/js-templates.md#data-attributes).
{% endhint %}

## Wiring the Template

The bindings need one element that owns the Alpine scope. Our root element is built by the hook, so instead we wrap the item loop in a new list `<div>` written in the template—where a single-quoted attribute can live—carrying `x-data`, the `x-bind` for the window listener, and the config. The hook's `classes` object gains a matching entry so the items keep their vertical gap inside the new wrapper:

```javascript
const classes = {
    // … wrapper and heading unchanged …
    list: ["flex flex-col", itemGap].filter(Boolean).join(" "),
    // … item, question, and answer unchanged …
};
```

Then update `templates/index.html`—the heading block is untouched, and the loop's markup changes only where Alpine takes over:

```html
<!-- templates/index.html — the loop, now inside the Alpine scope -->
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
            :aria-expanded="isOpen({{item.index}}).toString()"
            aria-controls="{{item.answerId}}"
            @click="toggle({{item.index}})"
        >
            <span>{{item.question}}</span>
            <span aria-hidden="true">+</span>
        </button>
        <div
            id="{{item.answerId}}"
            role="region"
            aria-labelledby="{{item.questionId}}"
            class="{{classes.answer}}"
            x-show="isOpen({{item.index}})"
            x-collapse
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
```

The Part 2 groundwork pays off here:

* **The ARIA ids just get rebound.** The static `aria-expanded="true"` from Part 2 becomes the live binding `:aria-expanded="isOpen({{item.index}}).toString()"`, while `id`, `aria-controls`, and `aria-labelledby` stay exactly as the hook computed them. The ARIA state now derives from the same reactive data as the visuals, so the two can never disagree—the principle behind [Accessibility Driven by Bindings](../interactive-components-with-alpine.md#accessibility-driven-by-bindings).
* **`x-show` + `x-collapse`** hide and reveal each answer. `x-show` toggles visibility from `isOpen()`; `x-collapse` (from the `alpine-collapse.js` plugin that's already loaded) upgrades the toggle into a smooth height animation. This is the same pairing as the Accordion's content panel.
* **Per-item expressions interpolate the index.** `toggle({{item.index}})` renders as `toggle(0)`, `toggle(1)`, and so on—build-time template values feeding runtime Alpine expressions, just like the Tabs template does with `activeTab === {{ tab.index }}`.

{% hint style="info" %}
Nothing changes on the edit canvas: component scripts don't run there, so Alpine never boots and every answer simply stays visible—which is exactly what editing needs. The published page is where the accordion comes alive, so check your work in **Preview**.
{% endhint %}

## Try It Out

Preview the page and click through the questions. Then exercise the configuration:

1. With **Allow Multiple Open** off, opening one question closes the others.
2. Turn it on—answers now stay open independently.
3. Toggle **First Item Open** and reload the preview to see item `0` start expanded or collapsed.
4. Add a second FAQ component to the page and confirm the two toggle independently—the `id` check in the window listener at work.

_[Screenshot: the published FAQ mid-transition, one answer expanding while another collapses]_

One rough edge remains: on a slow connection the published page briefly shows *every* answer open before Alpine boots and collapses them. Fixing that first paint—without breaking the always-open canvas—is where Part 4 begins.

## Checkpoint: Full Files So Far

`info.json`, `properties.json`, and the three collection files are unchanged from Part 2, and `templates/alpine.html` is new in this part—its complete contents are the wrapper plus the two factory listings from [The Factory in templates/alpine.html](#the-factory-in-templatesalpinehtml) above, combined:

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
    } = rw.props;
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

    const faqConfigJson = JSON.stringify({
        allowMultipleOpen: isOn(allowMultipleOpen),
        firstOpenOnLoad: isOn(firstOpenOnLoad),
    });

    const classes = {
        wrapper: [`group/${id}`, "flex flex-col", itemGap]
            .filter(Boolean)
            .join(" "),
        heading: "font-heading text-2xl text-text-900",
        list: ["flex flex-col", itemGap].filter(Boolean).join(" "),
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
        id,
        classes,
        questions: items,
        faqConfigJson,
    });
};

exports.transformHook = transformHook;
```

#### templates/index.html

```html
<!-- templates/index.html -->
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
            :aria-expanded="isOpen({{item.index}}).toString()"
            aria-controls="{{item.answerId}}"
            @click="toggle({{item.index}})"
        >
            <span>{{item.question}}</span>
            <span aria-hidden="true">+</span>
        </button>
        <div
            id="{{item.answerId}}"
            role="region"
            aria-labelledby="{{item.questionId}}"
            class="{{classes.answer}}"
            x-show="isOpen({{item.index}})"
            x-collapse
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
```

## Next Up

The FAQ behaves like a real accordion in the browser. Part 4 polishes everything around it: a first paint with no flash, an edit canvas that always shows every answer, placeholders for empty collections, dark-mode styling, an advanced-classes escape hatch, and `FAQPage` structured data:

{% content-ref url="part-4-edit-mode-and-polish.md" %}
[part-4-edit-mode-and-polish.md](part-4-edit-mode-and-polish.md)
{% endcontent-ref %}

## Related Documentation

* [Interactive Components with Alpine.js](../interactive-components-with-alpine.md)
* [JavaScript Templates](../../component/templates/js-templates.md)
* [@portal](../../component/language/portal.md)
* [Templates Overview](../../component/templates/README.md)
* [rw.setProps](../../component/hooks.js/available-functions/rw.setprops.md)
* [@if](../../component/language/if.md)
