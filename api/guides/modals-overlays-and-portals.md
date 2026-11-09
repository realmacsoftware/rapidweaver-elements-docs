---
description: Build overlay components that escape the layout using @portal
---

# Modals, Overlays & Portals

An overlay component lives a double life. The trigger — the button or badge the user clicks — belongs exactly where the user dropped the component, deep inside whatever grid, card, or slider they built. The panel it opens belongs somewhere else entirely: layered over the whole page, above everything. This guide walks through the complete anatomy of that split — an inline trigger, a panel teleported to `bodyEnd` with `@portal`, and an open/close signal that travels between them as a window-level event.

{% hint style="success" %}
This guide dissects the **Modal** (`com.realmacsoftware.modal`) and **Modal Close** (`com.realmacsoftware.modalClose`) components from the open-source [Core Pack](../development-resources/open-source-components.md). Open their source alongside this page.
{% endhint %}

## Why Overlays Break Inside the Layout

Render a full-screen panel where the component sits in the document and three CSS mechanisms conspire against you:

- **Ancestor `overflow`** — any ancestor with `overflow: hidden` or `overflow: auto` (sliders, cards, scroll areas) clips your panel to its own box.
- **Ancestor `transform`** — a transformed ancestor (scroll animations, hover effects) becomes the containing block for `position: fixed` descendants, so your "full-screen" panel positions itself relative to a card instead of the viewport.
- **Stacking contexts** — an ancestor with its own `z-index` and stacking context caps your panel's stacking order. No `z-index: 9999` on the panel can escape it; a sibling section later in the page can still paint on top.

You can't control any of this, because in Elements your component gets dropped into layouts you have never seen. The fix is not more CSS — it is moving the panel's markup out of the layout altogether. That is what [`@portal`](../component/language/portal.md) does: it transports a section of your template to a fixed page location. For overlays, the destination is `bodyEnd` — the end of the `<body>` element, outside every layout container, where `fixed` positioning and `z-index` behave predictably.

## Anatomy of the Core Modal

The Modal's `templates/index.html` is short enough to read whole, and it splits cleanly into the two halves described above.

### The Inline Trigger

The first half stays inline — it renders wherever the user drops the Modal:

```html
<!-- templates/index.html -->
<span
    @click="$dispatch('open-modal', { id: '{{id}}' })"
    class="{{classes.trigger}}"
>
    @dropzone("trigger", title: "Trigger")
</span>
```

The trigger is a [`@dropzone`](../component/language/dropzone.md), so the user decides what opens the modal — a Button, an Image, a line of text. Clicking anywhere in the span dispatches an `open-modal` event carrying this instance's id (more on that handshake below).

The `hooks.js` side wraps the whole component in an Alpine scope and wires up the optional auto-open behaviours:

```javascript
// hooks.source.js (excerpt)
const { id } = rw.node;

rw.setRootElement({
    as: "div",
    class: classes.wrapper,
    args: {
        "x-data": `{ open: false, openModal: () => $dispatch('open-modal', { id: '${id}' }) }`,
        "x-init": `${
            autoOpen
                ? `setTimeout(() => openModal(), ${autoOpenTime})`
                : null
        }`,
        "x-exit-intent": openOnExitIntent ? "openModal" : null,
        id: globalID,
    },
});

// …

rw.setProps({
    classes,
    id,
    transitionAttributes,
});
```

Note that both the click handler and the root scope's `openModal()` do the same thing: dispatch `open-modal` with the instance id. Auto-open on page load, after a delay, or on exit intent all reuse the one function. (Helpers like `classnames` and `getAlpineTransitionAttributesMobile` are shared Core Pack utilities bundled into the compiled `hooks.js` at build time — `hooks.source.js` is the authored source.)

### The Teleported Panel

The second half of the template never renders where the component sits. It is wrapped in `@portal("bodyEnd")`, so Elements transports it to the end of `<body>`:

```html
<!-- templates/index.html -->
@portal("bodyEnd")
<div
    x-dialog
    @if(!edit)
    x-cloak
    @endif
    x-data="{ 
        open: false,
        stopAllMedia() {
            this.$el.querySelectorAll('video, audio').forEach(media => {
                media.pause();
                media.currentTime = 0;
            });
            this.$el.querySelectorAll('iframe').forEach(iframe => {
                const src = iframe.src;
                iframe.src = '';
                iframe.src = src;
            });
        }
    }"
    x-init="$watch('open', value => { if (!value) { stopAllMedia(); } })"
    @open-modal.window="(e) => { open = e.detail.id === '{{id}}' }"
    x-model="open"
    class="{{classes.dialog}}"
    data-modal-id="{{id}}"
>
    <div
        x-dialog:overlay
        x-transition.opacity
        class="{{classes.overlay}}"
    ></div>

    <div @click.stop="open = false" class="{{classes.panel}}">
        <div
            @click.stop
            x-dialog:panel
            {{transitionAttributes}}
            class="{{classes.panelInner}}"
        >
            @dropzone("content", title: "Content")
        </div>
    </div>
</div>
@endportal
```

Walking through it:

- **`@portal("bodyEnd") … @endportal`** — the whole dialog lands at the end of `<body>`. There is deliberately no `includeOnce` here: unlike a shared `<script>` portal, this block is per-instance markup, and every Modal on the page needs its own panel at `bodyEnd`. (The destination can be written bare or quoted — `@portal(bodyEnd)` and `@portal("bodyEnd")` are equivalent.)
- **`x-dialog`** — the headless dialog behaviour from the Core Pack's shared Alpine UI plugin (`shared/assets/alpine-ui.js`). It contributes focus trapping, Escape-to-close, and the `x-dialog:overlay` / `x-dialog:panel` roles on the inner elements. `x-model="open"` binds the plugin's open state to the local `open` variable, so writing `open = true` opens the dialog and the plugin closing it (Escape, `$dialog.close()`) writes `false` back.
- **`@open-modal.window="(e) => { open = e.detail.id === '{{id}}' }"`** — the receiving end of the trigger's dispatch. The `.window` modifier listens at the window level, which is what makes the whole scheme work (next section).
- **The overlay and panel** — a fixed, tinted overlay (`x-transition.opacity` fades it) behind a centred panel. Clicking the panel wrapper closes the modal; `@click.stop` on the inner panel stops clicks on the content from bubbling up and closing it. The `content` dropzone travels with the portal, so everything the user drops into the modal renders inside the teleported panel.
- **`stopAllMedia()`** — a real-world nicety: a `$watch` on `open` pauses any `<video>`/`<audio>` and resets `<iframe>` embeds when the modal closes, so a playing YouTube embed doesn't keep blaring behind a closed modal.

## The Id Handshake

Why does the event carry an id at all? Because the portal severs the DOM relationship between the two halves. Once the dialog is teleported to `bodyEnd`, it is no longer a descendant of the component's root element — so it cannot inherit the trigger's Alpine scope, and the trigger cannot reach it through `$refs` or shared `x-data`. A window-level event is the reliable channel between two elements that are no longer related in the DOM.

But window-level means *every* modal's listener hears *every* `open-modal` event. The handshake sorts it out:

1. The trigger dispatches `open-modal` with `{ id: '{{id}}' }` — the instance id from `rw.node.id`, unique per Modal on the page.
2. Every dialog's listener runs `open = e.detail.id === '{{id}}'`, comparing against its own instance id.

Only the matching dialog gets `open = true`. And note the elegant side effect of assigning the comparison result rather than guarding with it: every *non-matching* modal sets `open = false`, so opening one modal automatically closes any other — at most one modal is ever open, with no coordination code.

## Edit Mode: Keeping the Panel on the Canvas

A modal that only exists after a click would be unusable in the editor — the user could never fill its `content` dropzone. The Modal handles edit mode with two small, deliberate moves.

First, the `x-cloak` that hides the dialog until Alpine boots is applied *only outside edit mode*:

```html
@if(!edit)
x-cloak
@endif
```

In a published page, `x-cloak` prevents the dialog from flashing on screen before Alpine initialises and hides it. On the edit canvas, the attribute is omitted so the panel can render and be edited directly.

Second, `hooks.js` adjusts the dialog and overlay classes when the project is in edit mode:

```javascript
// hooks.source.js (excerpt)
const { mode } = rw.project;

const classes = {
    // …
    dialog: classnames([
        "fixed z-50 inset-0 overflow-y-auto",
        !modalShowInEdit && mode === "edit" && "hidden",
    ]).toString(),
    // …
    overlay: classnames([
        "fixed inset-0 bg-black/25",
        // …
        mode === "edit" && "pointer-events-none",
    ]).toString(),
};
```

`modalShowInEdit` is a **Show** switch in the Modal's `properties.json`. When it is off in edit mode, the dialog gets `hidden` — the canvas shows just the trigger, as the published page would. When it is on, the panel appears on the canvas for editing, and the full-screen overlay gets `pointer-events-none` so it never swallows clicks meant for the canvas underneath. This give-the-user-a-toggle pattern — and edit-mode canvas behaviour in general — is covered in depth in [Edit Mode Experience](./edit-mode-experience.md).

## Pairing Components: Modal Close

Opening is only half the contract. The Core Pack ships a companion component, **Modal Close** (`com.realmacsoftware.modalClose`), that the user drops *inside* the modal's content to close it from anywhere — a styled button, an X icon in the corner, a "No thanks" text link. It is tiny; this is essentially the whole component:

```javascript
// hooks.source.js (excerpt)
const transformHook = (rw) => {
    const { closeCursor } = rw.props;
    // …

    const classes = classnames([
        `relative z-50 cursor-pointer`,
        closeCursor,
    ]).toString();

    rw.setRootElement({
        as: "div",
        class: classes,
        args: {
            "@click": "$dialog.close()",
        },
    });
    // …
};

exports.transformHook = transformHook;
```

```html
<!-- templates/index.html -->
@dropzone("modalClose", title: "Modal Close")
```

The entire component is a click surface around a dropzone. It works because of *where it renders at runtime*: dropped into the Modal's `content` dropzone, it travels with the portal into the teleported dialog, so in the final DOM it is a descendant of the `x-dialog` element. Alpine's `$dialog` magic (from the same shared plugin) resolves to the nearest enclosing dialog and closes it — no id handshake needed on the way out, because DOM ancestry is intact inside the panel.

This trigger/receiver pairing — one component dispatching or acting, a sibling component designed to live inside it — generalises well beyond modals. See [Component Suites](./component-suites.md) for the full pattern.

## Variations on the Skeleton

The Modal's skeleton — inline trigger, `@portal("bodyEnd")` panel, window event with an id payload, `@if(!edit)`-gated `x-cloak` — is a template for any overlay. Two sketches show how little changes. Both are plain Alpine (no `x-dialog` plugin), so they handle their own Escape key and dismissal.

### Off-Canvas Drawer

Same skeleton; only the positioning and transition classes change — the panel pins to the viewport edge and slides instead of fading:

```html
<!-- com.example.drawer — templates/index.html -->
<span @click="$dispatch('open-drawer', { id: '{{id}}' })" class="cursor-pointer">
    @dropzone("trigger", title: "Trigger")
</span>

@portal("bodyEnd")
<div
    @if(!edit)
    x-cloak
    @endif
    x-data="{ open: false }"
    x-show="open"
    @open-drawer.window="(e) => { open = e.detail.id === '{{id}}' }"
    @keydown.escape.window="open = false"
    class="fixed inset-0 z-50"
>
    <div @click="open = false" class="fixed inset-0 bg-black/40"></div>
    <aside
        x-show="open"
        x-transition:enter="transition ease-out duration-300"
        x-transition:enter-start="translate-x-full"
        x-transition:enter-end="translate-x-0"
        x-transition:leave="transition ease-in duration-200"
        x-transition:leave-start="translate-x-0"
        x-transition:leave-end="translate-x-full"
        class="fixed inset-y-0 right-0 w-80 max-w-full overflow-y-auto bg-white shadow-xl"
    >
        @dropzone("content", title: "Drawer Content")
    </aside>
</div>
@endportal
```

### Toast Notification

A toast drops the blocking overlay entirely and adds an auto-dismiss timer. The timer needs cleanup: clear any pending timeout before arming a new one, so rapid re-triggers extend the toast instead of letting a stale timer dismiss it early:

```html
<!-- com.example.toast — templates/index.html -->
<span @click="$dispatch('show-toast', { id: '{{id}}' })" class="cursor-pointer">
    @dropzone("trigger", title: "Trigger")
</span>

@portal("bodyEnd")
<div
    @if(!edit)
    x-cloak
    @endif
    x-data="{
        open: false,
        timer: null,
        show() {
            clearTimeout(this.timer);
            this.open = true;
            this.timer = setTimeout(() => { this.open = false }, {{toastDurationMs}});
        }
    }"
    x-show="open"
    x-transition.opacity
    @show-toast.window="(e) => { if (e.detail.id === '{{id}}') show() }"
    class="fixed bottom-4 right-4 z-50 rounded-lg bg-black/80 px-4 py-3 text-white shadow-lg"
>
    @dropzone("content", title: "Toast Content")
</div>
@endportal
```

The duration comes from a number property, converted to milliseconds in the hook:

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const seconds = rw.props.toastDuration ?? 4;
    rw.setProps({ toastDurationMs: seconds * 1000 });
};
```

Note the toast guards with `if (e.detail.id === '{{id}}')` rather than assigning the comparison — unlike modals, several toasts may legitimately be visible at once, so a non-matching event should leave other toasts alone. For richer Alpine behaviour in overlays — shared factories, `alpine:init` registration, passing structured config — see [Interactive Components with Alpine](./interactive-components-with-alpine.md) and [JavaScript Templates](../component/templates/js-templates.md).

## Related Documentation

- [`@portal` Directive](../component/language/portal.md) — destinations, `includeOnce`, and deduplication ids
- [`@dropzone` Directive](../component/language/dropzone.md) — user-fillable regions like the trigger and content
- [Interactive Components with Alpine](./interactive-components-with-alpine.md) — Alpine patterns used throughout this guide
- [Edit Mode Experience](./edit-mode-experience.md) — designing components that behave well on the canvas
- [JavaScript Templates](../component/templates/js-templates.md) — shipping scripts through portals
