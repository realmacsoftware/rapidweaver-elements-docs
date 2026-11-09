---
description: Build a form suite with a parent form, field children, and a secure PHP backend
---

# Building Form Components

Forms pull together everything the other guides cover in isolation: a parent/child suite, native browser validation, an Alpine-driven submit flow, and a PHP endpoint that must treat every byte it receives as hostile. This guide assembles all of it into one complete, working architecture — a parent form component, independent field children, and a backend that validates, filters spam, sends mail, and forwards to webhooks.

{% hint style="info" %}
Unlike the other guides in this section, this one doesn't dissect a core-pack component — the open-source Core Pack has no form suite. Instead it presents a **reference architecture**: freshly written `com.example.*` code that scales up the contact-form example from the [Backend reference](../component/templates/backend.md) by combining the parent/child contract from [Component Suites](./component-suites.md) with the server-side patterns from [Server-Side PHP Components](./server-side-php-components.md).
{% endhint %}

## The Architecture

One component per responsibility. The parent owns the `<form>` element, the submit flow, and the backend endpoint; each field is an independent child the user drops into the parent's dropzone:

```
com.example.formpack/
├── components/
│   ├── com.example.form/            # the parent
│   │   ├── info.json                #   requiresPhp: true
│   │   ├── properties.json          #   submitLabel, notificationEmail, requiredFields…
│   │   ├── hooks.js
│   │   └── templates/
│   │       ├── index.html           #   <form>, fields dropzone, honeypot, button, status
│   │       ├── alpine.html          #   the submit factory (portal)
│   │       └── backend/
│   │           └── submit.php       #   validation, spam checks, mail, webhook
│   ├── com.example.textField/       # a field child: <label> + <input>
│   │   ├── properties.json
│   │   ├── hooks.js
│   │   └── templates/
│   │       └── index.html
│   └── com.example.selectField/     # same contract, renders a <select>
└── shared/
    └── assets/                      # optional: an SMTP library (see Sending Mail)
```

You could build this as one mega-component whose inspector defines every field — but you'd be rebuilding the editor inside an inspector. The number of fields is unpredictable, each field needs its own settings, and a plain [`@dropzone`](../component/language/dropzone.md) filling is inert — the moment a field needs an inspector and validation of its own, it has to be a component. These are exactly the split criteria from [Component Suites](./component-suites.md#when-one-component-should-become-several).

What makes a form suite unusually easy to wire is that **the parent never enumerates its children**. The browser does it: any control inside a `<form>` that carries a `name` attribute is serialised into `FormData` automatically, and PHP receives the same set as `$_POST`. The suite contract collapses to "render a named input inside the form" — the DOM-ancestry channel from the suites guide, with native form serialisation doing the transport.

## The Parent: com.example.form

The parent's hooks resolve the mode, its instance id, and — crucially — pass `rw.node` through so the template can point the form at the backend folder via [`rw.node.backendPath`](../component/hooks.js/available-data/rw.node.md), the same pattern the [Backend reference](../component/templates/backend.md#using-nodebackendpath) uses:

```javascript
// com.example.form — hooks.js
const transformHook = (rw) => {
    const { id } = rw.node;
    const { submitLabel, successMessage, errorMessage } = rw.props;

    rw.setProps({
        id,
        edit: rw.project.mode === "edit",
        node: rw.node, // exposes {{node.backendPath}} to the template
        submitLabel: submitLabel || "Send",
        successMessage: successMessage || "Thanks — your message has been sent.",
        errorMessage: errorMessage || "Something went wrong. Please try again.",
        classes: {
            form: "flex flex-col gap-4",
            button: "self-start rounded bg-blue-600 px-4 py-2 text-white disabled:opacity-50",
            success: "rounded bg-green-100 px-3 py-2 text-sm text-green-900",
            error: "rounded bg-red-100 px-3 py-2 text-sm text-red-900",
        },
    });
};

exports.transformHook = transformHook;
```

The template renders the form element itself, the fields dropzone, a hidden honeypot and metadata input, the submit button, and two status regions:

```html
<!-- com.example.form — templates/index.html -->
<form
    x-data="exampleForm()"
    data-form-id="{{id}}"
    action="{{node.backendPath}}/submit.php"
    method="post"
    @if(!edit)
    @submit.prevent="submit"
    @endif
    class="{{classes.form}}"
>
    @dropzone("fields", title: "Fields")

    <!-- Honeypot — visually hidden, real visitors never fill it -->
    <label class="hidden" aria-hidden="true">Leave this field empty
        <input type="text" name="website" tabindex="-1" autocomplete="off">
    </label>

    <!-- Metadata for the backend -->
    <input type="hidden" name="_form" value="{{id}}">

    <button type="submit" :disabled="submitting" class="{{classes.button}}">
        <span x-show="!submitting">{{submitLabel}}</span>
        <span x-show="submitting">Sending&hellip;</span>
    </button>

    <p x-show="status === 'success'" role="status" class="{{classes.success}}">{{successMessage}}</p>
    <p x-show="status === 'error'" role="alert" class="{{classes.error}}">{{errorMessage}}</p>
</form>
```

Three details to note. The `action` and `method` attributes make the form work even before (or without) JavaScript — the Alpine layer is an enhancement, not a requirement. The `data-form-id` attribute is the parent's half of the [DOM-ancestry contract](./component-suites.md#parent-child-contracts-without-events), there for any child that needs to discover its form at runtime. And the `@if(!edit)` block around `@submit.prevent` is the edit-mode gate — more on that below. (`@submit.prevent` itself is Alpine shorthand, not an Elements directive; it passes through the template engine untouched.)

## The Field Contract

A field child can be anything, from any pack, as long as it honours four rules:

1. **Render exactly one form control with a `name` attribute.** That name is the key the backend receives in `$_POST` — it's the entire data contract.
2. **Give the control a unique `id` and point a `<label for="…">` at it.** Derive the id from the node id so two instances never collide.
3. **Express validation as native attributes** — `required`, `type="email"`, `pattern` — so the browser, the parent's Alpine factory, and assistive technology all see the same rules.
4. **Stay out of the reserved namespace.** Never start a field name with `_` (the parent's metadata prefix) and never reuse the honeypot's name.

Here is `com.example.textField` in full — properties, hooks, template:

```json
// com.example.textField — properties.json
{
    "groups": [{
        "title": "Field",
        "properties": [{
            "title": "Label",
            "id": "label",
            "text": { "default": "Name" }
        }, {
            "title": "Field Name",
            "id": "fieldName",
            "text": {
                "default": "name",
                "subtitle": "The key this value is submitted under"
            }
        }, {
            "title": "Type",
            "id": "fieldType",
            "responsive": false,
            "select": {
                "default": "text",
                "items": [
                    { "value": "text", "title": "Text" },
                    { "value": "email", "title": "Email" },
                    { "value": "tel", "title": "Phone" }
                ]
            }
        }, {
            "title": "Required",
            "id": "required",
            "responsive": false,
            "switch": { "default": false }
        }]
    }]
}
```

```javascript
// com.example.textField — hooks.js
const transformHook = (rw) => {
    const { id } = rw.node;
    const { label, fieldName, fieldType, required } = rw.props;

    rw.setProps({
        inputId: `field-${id}`,
        label: label || "Field",
        fieldName: fieldName || `field-${id}`,
        fieldType: fieldType || "text",
        isRequired: required === true,
        classes: {
            wrapper: "flex flex-col gap-1",
            label: "text-sm font-medium",
            input: "rounded border border-gray-300 px-3 py-2",
        },
    });
};

exports.transformHook = transformHook;
```

```html
<!-- com.example.textField — templates/index.html -->
<div class="{{classes.wrapper}}">
    <label for="{{inputId}}" class="{{classes.label}}">{{label}}</label>
    <input
        id="{{inputId}}"
        type="{{fieldType}}"
        name="{{fieldName}}"
        @if(isRequired)
        required
        @endif
        class="{{classes.input}}"
    >
</div>
```

The **Type** select is validation-as-property: choosing *Email* emits `type="email"`, and the browser validates the format for free. To support custom formats, add a `pattern` text property and emit it the same way as `required` — an `@if(hasPattern)` wrapping a `pattern="{{pattern}}"` attribute (precompute `hasPattern` in hooks; `@if` takes a single condition). A `com.example.selectField` follows the identical contract with a `<select>` element — build its `<option>` list from a collection, as shown in [Collection-Driven Dropzones](./collection-driven-dropzones.md). And since a field dropped outside any form silently does nothing, give children the edit-mode orphan banner from [Component Suites](./component-suites.md#packaging-a-suite).

## Submission UX with Alpine

The parent's Alpine factory lives in `templates/alpine.html` — a root-level template, so Elements processes it automatically alongside `index.html`. It drives the whole visitor-facing flow: validate, disable the button, `fetch()` the backend, and surface the result:

```html
<!-- com.example.form — templates/alpine.html -->
@portal(bodyEnd, includeOnce: true, id: "com.example.form.alpine")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("exampleForm", () => ({
            submitting: false,
            status: "idle",
            async submit() {
                const form = this.$el;

                // Native validation first: it already knows about every
                // required/type/pattern attribute the field children emitted.
                if (!form.checkValidity()) {
                    const firstInvalid = form.querySelector(":invalid");
                    if (firstInvalid) firstInvalid.focus();
                    form.reportValidity();
                    return;
                }

                this.submitting = true;
                this.status = "idle";

                try {
                    // FormData picks up every named control in the form —
                    // including fields from children the parent knows nothing about.
                    const response = await fetch(form.action, {
                        method: "POST",
                        body: new FormData(form),
                        headers: { Accept: "application/json" },
                    });
                    const result = await response.json();

                    if (response.ok && result.success) {
                        this.status = "success";
                        form.reset();
                    } else {
                        this.status = "error";
                    }
                } catch (error) {
                    this.status = "error";
                } finally {
                    this.submitting = false;
                }
            },
        }));
    });
</script>
@endportal
```

`submitting` disables the button (`:disabled`) and swaps its label; `status` reveals exactly one of the two status regions. On failure the form keeps the visitor's input — only success resets it.

One thing this factory deliberately does *not* do is run on the canvas: the `@if(!edit)` in the parent template strips `@submit.prevent` in edit mode, so clicking **Send** while editing never fires a `fetch()` at a backend that doesn't exist yet. Everything visual — the button, the fields, the layout — stays fully styleable on the canvas. That's the *gate behaviour, keep styling visible* discipline from [Designing the Edit-Mode Experience](./edit-mode-experience.md#gating-heavy-behaviour-on-the-canvas).

## The Backend: submit.php

The endpoint extends the contact-form example from the [Backend reference](../component/templates/backend.md) into something production-shaped: method check, honeypot, server-side required fields, sanitisation, and JSON responses with meaningful status codes. `notificationEmail` and `requiredFields` (a comma-separated list of field names) are text properties on the parent — publish time can't know which children the user dropped in, so the user declares which names the server must enforce:

```php
<!-- templates/backend/submit.php -->
<?php
header('Content-Type: application/json');

// Frozen in at publish time by Elements
$notificationEmail = '{{notificationEmail}}';
$requiredFields    = array_filter(array_map('trim', explode(',', '{{requiredFields}}')));

if ($_SERVER['REQUEST_METHOD'] !== 'POST') {
    http_response_code(405);
    echo json_encode(['success' => false, 'error' => 'Method not allowed']);
    exit;
}

// 1. Honeypot: a filled trap field means a bot. Claim success so it moves on.
if (!empty($_POST['website'])) {
    echo json_encode(['success' => true]);
    exit;
}

// 2. Required fields, enforced server-side. Client-side `required` is UX, not security.
$missing = [];
foreach ($requiredFields as $field) {
    if (trim($_POST[$field] ?? '') === '') {
        $missing[] = $field;
    }
}
if (!empty($missing)) {
    http_response_code(422);
    echo json_encode(['success' => false, 'error' => 'Missing required fields', 'fields' => $missing]);
    exit;
}

// 3. Sanitise every value; drop the trap field, metadata keys, and non-strings
$data = [];
foreach ($_POST as $key => $value) {
    if ($key === 'website' || substr($key, 0, 1) === '_' || !is_string($value)) {
        continue;
    }
    $data[$key] = htmlspecialchars(strip_tags(trim($value)), ENT_QUOTES, 'UTF-8');
}

// 4. Validate any email field properly
if (isset($data['email']) && filter_var($data['email'], FILTER_VALIDATE_EMAIL) === false) {
    http_response_code(422);
    echo json_encode(['success' => false, 'error' => 'Invalid email address']);
    exit;
}

// 5. Notify and answer
$lines = [];
foreach ($data as $key => $value) {
    $lines[] = $key . ': ' . $value;
}
$sent = mail($notificationEmail, 'Form submission', implode("\n", $lines));
echo json_encode(['success' => $sent]);
```

Everything arriving in `$_POST` is untrusted request-time data, so it's escaped with `htmlspecialchars(…, ENT_QUOTES, 'UTF-8')` before it goes anywhere near an email body or a webhook payload — the same rule as [A Note on Escaping](./server-side-php-components.md#a-note-on-escaping). The status codes matter too: the Alpine factory treats any non-2xx response as failure, so `422` for validation problems and `405` for stray GETs give you correct front-end behaviour with no extra client code.

## Spam Protection

### The Honeypot

The honeypot is already fully wired above; here's why it works. The parent renders a text input named `website` inside a container hidden with `class="hidden"` and `aria-hidden="true"`, with `tabindex="-1"` and `autocomplete="off"` so neither keyboard users nor browser autofill ever touch it. Humans can't see the field, so it always arrives empty; unsophisticated bots fill every input they find, so a non-empty value is a reliable bot signal. The backend then *claims success* rather than returning an error — a rejection teaches a bot author what to fix, while a fake success ends the conversation. Pick a trap name that looks worth filling (`website`, `company`) rather than one that advertises itself, and make sure no real field child ever uses it.

### CAPTCHA Services

For heavier abuse you can layer a CAPTCHA service on top. Whatever provider you choose, the shape is always the same round-trip:

1. A widget script runs in the browser, and once the challenge passes it writes a **token** into a hidden input inside your form — `FormData` carries it to your backend automatically.
2. `submit.php` reads the token and makes a **server-to-server verification call** to the provider, sending the token plus your **secret key**.
3. Only if the provider confirms the token do you process the submission; otherwise return `422` like any other validation failure.

The provider gives you two keys, and they must be handled differently. The **site key** is designed to be public — it ends up in your rendered HTML no matter what — so a text property on the form component is the right home for it. The secret key is another matter:

{% hint style="warning" %}
Property values are interpolated into published files at publish time, so anything a user types into the inspector ships with the site. Only **publishable (site) keys** belong in component properties — never secret keys. Instruct users to put the secret key directly in the backend file on the server, or better, in the hosting environment (read it with `getenv()`), where it never passes through the project file or the publish pipeline.
{% endhint %}

## Sending Mail

The `mail()` call above is the honest weak point of the example: it hands the message to whatever local mail transport the host provides, with no SMTP authentication and often a misconfigured envelope sender — so on real-world shared hosting, messages regularly land in spam or vanish, and some hosts disable `mail()` outright. The robust upgrade is an SMTP library authenticating against a real mailbox. Don't put a multi-file library inside `templates/backend/` — Elements watches every backend file for changes, which hurts performance. Ship it in your pack's [shared assets](../component/shared-files/assets.md) and `require_once` it from `submit.php` via `siteAssetPath`, exactly as the [Backend reference](../component/templates/backend.md) shows for large PHP libraries. The trade-offs are the same as the vendoring decision table in [Integrating JavaScript Libraries](./integrating-javascript-libraries.md#where-library-files-live): one shared copy for the whole pack, referenced from every component that needs it.

## Forwarding to a Webhook

Email is for humans; automations want JSON. Forwarding the sanitised `$data` array to a user-configured webhook URL (a `webhookUrl` text property) takes one curl call at the end of `submit.php`, after the mail step:

```php
<!-- templates/backend/submit.php (appended after the mail() call) -->
<?php
$webhookUrl = '{{webhookUrl}}';
if ($webhookUrl !== '') {
    $ch = curl_init($webhookUrl);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_POST, true);
    curl_setopt($ch, CURLOPT_HTTPHEADER, ['Content-Type: application/json']);
    curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
    curl_setopt($ch, CURLOPT_TIMEOUT, 10);
    curl_exec($ch);
    curl_close($ch);
}
```

Note the snippet ignores the response and never fails the visitor's submission over a webhook problem — the email is the primary record. That's also the caveat: this is fire-once with **no retry**. If the endpoint is down for ten seconds, that event is gone. For genuinely mission-critical integrations, point the webhook at a service that queues and retries on its own, rather than teaching `submit.php` to persist state.

## requiresPhp and the Suite

Declare `requiresPhp: true` in `com.example.form`'s `info.json`. Strictly speaking the endpoint runs as its own request — the browser fetches `submit.php` directly — but the flag declares the suite's real dependency on a PHP-capable host, and the moment the form grows any server-rendered markup on the page itself (a CSRF token, a server-rendered thank-you state) the page *must* publish as `.php`. The children need nothing: per the [`info.json` reference](../component/info.json.md), the flag isn't needed for child components that only ever appear nested inside a component that already requires PHP. But inheritance doesn't travel — a field child that can also be placed standalone must declare the flag itself. The full rules, including that standalone caveat worked through, are in [Server-Side PHP Components](./server-side-php-components.md#declaring-requiresphp).

## Related Documentation

* [Backend Directory](../component/templates/backend.md) — deployment structure, `node.backendPath`, and the seed contact-form example
* [Component Suites & Cross-Component Communication](./component-suites.md) — when to split, and the parent/child contract
* [Server-Side PHP Components](./server-side-php-components.md) — `requiresPhp`, escaping, and request-time PHP
* [Designing the Edit-Mode Experience](./edit-mode-experience.md) — gating behaviour on the canvas
* [@dropzone](../component/language/dropzone.md) — the directive behind the fields area
