---
description: Turn a child Button or similar component into the form submission control
---

# Submit

Submit provides the behaviour that validates and submits its parent Form. It is a wrapper with a drop zone; it does not draw a visible control of its own.

{% hint style="danger" %}
**Submit does not work on its own.** Add a Button, Image, or another visible and clearly clickable component inside its drop zone. Without a child component, visitors have nothing to click and the form will not submit.
{% endhint %}

### How to Use Submit

You’ll find Submit under **Forms** in the Components list.

1. Place Submit inside a [Form](README.md).
2. Drag a **Button** into Submit’s drop zone.
3. Edit the Button text—for example, “Send message”.
4. Leave the Button’s Link unset so it does not navigate away.
5. Add [Success](success.md) and [Error](error.md) content to the Form.
6. Publish and test validation, loading, success, and failure behaviour.

Button is the recommended child because it gives visitors familiar semantics, focus behaviour, and a clear click target. Another component can be used when it remains keyboard accessible and its purpose is obvious.

### Component Settings

Submit has no component-specific Inspector settings. Its child component controls appearance, size, text, hover, focus, and accessibility.

Advanced Classes and ID are available on the Submit wrapper.

### How Submission Works

Clicking the child component asks the parent Form to:

1. Check browser validation and Required fields.
2. Display invalid-field styling when needed.
3. Collect field values and attachments.
4. Send the data to the configured Email or Webhook endpoint.
5. Show Success or Error content, or follow the configured redirect.

### Accessibility

Use a Button with an action label such as “Send message”, “Create account”, or “Request quote”. Avoid vague labels such as “Click here”. Keep the control reachable and operable with a keyboard.

### Troubleshooting

#### Clicking Submit does nothing

Confirm that:

* A Button or similar clickable component is inside Submit.
* Submit is inside Form.
* The child Button does not have a Link destination.
* The form is being tested on a published PHP-enabled server.

#### The Button navigates away

Clear the child Button’s Link. Submit supplies the action; the Button does not need its own destination.

### Related Components

* [Form](README.md) — Configures validation and delivery.
* [Success](success.md) — Shows successful-submission content.
* [Error](error.md) — Shows failure content.

{% include "../../../.gitbook/includes/common-controls.md" %}
