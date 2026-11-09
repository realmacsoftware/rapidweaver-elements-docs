---
description: Build a complete FAQ accordion component from scratch in four hands-on parts
icon: list-check
---

# Tutorial: Build an FAQ Component

In this tutorial you'll build a production-quality FAQ accordion—`com.example.faq`—from an empty folder to a themed, interactive component that emits structured data for search engines. Each part ends with complete, working files, so you can stop after any part and still have a component that runs.

{% hint style="success" %}
Every pattern here comes from the open-source [Core Pack](../../development-resources/open-source-components.md). The relevant core component is named and linked at each step—keep its source open alongside the tutorial and compare as you go.
{% endhint %}

## What You'll Build

An FAQ component whose questions are managed in the inspector, styled by the theme, and rendered as an accessible accordion:

* **Collection-driven content** — users add, edit, and reorder questions in a dedicated inspector panel
* **Theme-aware styling** — accent color, item gap, corner radius, and question text style all resolve through Theme Studio controls
* **Flexible answers** — each answer is plain text by default, or a full dropzone that accepts any other component
* **Accordion behavior** — one-open-at-a-time (or allow multiple), optional first-item-open-on-load, and smooth collapse transitions via Alpine.js
* **Editor-friendly** — every answer stays open on the edit canvas, and placeholder questions appear while the collection is empty
* **SEO-ready** — emits `FAQPage` JSON-LD structured data into the page head

## The Finished Files

By the end of Part 4 the component folder looks like this:

```
com.example.faq/
├── info.json
├── properties.json
├── collections/
│   └── questions/
│       ├── info.json
│       ├── properties.json
│       └── defaults.json
├── hooks.js
└── templates/
    ├── index.html
    └── alpine.html
```

## Prerequisites

You should have Elements installed with a Dev Pack you can edit, and know how to add a component to a page and preview it. The Quickstart covers all of that, including short videos on creating a pack and editing its files:

{% content-ref url="../../getting-started/getting-started.md" %}
[getting-started.md](../../getting-started/getting-started.md)
{% endcontent-ref %}

A passing familiarity with Tailwind CSS helps but isn't required—[Component Styling](../../component/component-styling.md) explains the utility-class approach the tutorial follows, and there is no build step to set up.

## How the Four Parts Stack

The parts build on each other in order. Each one starts from the exact files the previous part ended with:

1. [Part 1: Scaffolding & Properties](part-1-scaffolding-and-properties.md) — create the component folder, describe it in `info.json`, define every inspector control in `properties.json`, compose theme-driven classes in a minimal `hooks.js`, and render a static two-question accordion.
2. [Part 2: Collections & Dynamic Dropzones](part-2-collections-and-dropzones.md) — replace the hard-coded questions with a `questions` collection, precompute per-item IDs and ARIA attributes in hooks, and let individual answers switch between plain text and a dropzone.
3. [Part 3: Interactivity with Alpine.js](part-3-interactivity.md) — register an Alpine.js factory through `@portal(bodyEnd)`, wire up open/close state with one-open-at-a-time behavior, pass configuration through a data attribute, and add `x-collapse` transitions.
4. [Part 4: Edit Mode, Theming & Polish](part-4-edit-mode-and-polish.md) — keep all answers open on the canvas with `@if(edit)`, show placeholder items while the collection is empty, and emit `FAQPage` JSON-LD via `@portal(headEnd)`.

If you only need one technique—say, collection-driven dropzones—you can read that part on its own. The "files so far" listings at the end of each part let you catch up without retyping every step.

## Conventions Used in the Tutorial

A few things to know before you start:

* **Code listings are complete.** Multi-file examples name the file in a comment on the first line (`// hooks.js`, `<!-- templates/index.html -->`) or in the heading above the block—type them in exactly as shown.
* **Checkpoints end every part.** Compare your files against the checkpoint before moving on; each part assumes the previous checkpoint verbatim.
* **Core Pack references are real.** When a step says a pattern comes from Tabs, Table, or Accordion, that component's source in the open-source Core Pack contains the original—reading it alongside the tutorial is the fastest way to level up.
* **No build tools required.** Everything is plain JSON, HTML, and JavaScript. The core components use the optional [Build Tools](../../development-resources/build-tools/README.md) helpers at a larger scale, but nothing here depends on them.

## Related Documentation

* [Quickstart](../../getting-started/getting-started.md)
* [What is a Component?](../../component/components.md)
* [Component Styling](../../component/component-styling.md)
* [Properties](../../component/properties.json/README.md)
* [Collections](../../component/collections/README.md)
* [Elements Language](../../component/language/README.md)
* [Open Source Components](../../development-resources/open-source-components.md)
