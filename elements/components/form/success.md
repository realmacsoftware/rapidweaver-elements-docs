---
description: Show custom content after a successful form submission
---

# Success

Success is a conditional drop zone shown after the parent Form receives a successful response. Add text, icons, Containers, or other components to create the confirmation visitors should see.

### How to Use Success

You’ll find Success under **Forms** in the Components list.

1. Place Success inside a [Form](README.md).
2. Add a Text component with a clear confirmation.
3. Optionally explain what happens next or when the visitor should expect a reply.
4. Use Preview in Edit while designing.
5. In Form, keep On Success set to Success Content.
6. Publish and complete a real submission.

### Component Settings

**Preview in Edit** is enabled by default. It controls only the editor preview; published Success content remains hidden until submission succeeds.

Success has no other component-specific Inspector settings. Its child components control the confirmation’s content and styling.

The parent Form’s **Reset** setting is enabled by default and clears fields after success.

{% hint style="info" %}
Success is not shown when Form → On Success is set to Redirect. In that mode, the configured Link is opened instead.
{% endhint %}

### Accessibility

Use clear confirmation language and explain the next step. Do not rely on a checkmark or green colour alone to communicate success.

### Related Components

* [Error](error.md) — Shows content after failure.
* [Submit](submit.md) — Provides the clickable submission control.
* [Form](README.md) — Controls Success Content, Redirect, and Reset.

{% include "../../../.gitbook/includes/common-controls (1).md" %}
