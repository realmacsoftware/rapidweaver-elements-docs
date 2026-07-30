---
description: Show custom content when a form fails
---

# Error

Error is a conditional drop zone shown when form submission fails. Add text, icons, Containers, or other components to create the message visitors should see. Browser validation messages and the Form component’s invalid-field colours handle missing or invalid field values before submission.

### How to Use Error

You’ll find Error under **Forms** in the Components list.

1. Place Error inside a [Form](README.md).
2. Add a Text component with a clear failure message.
3. Optionally add recovery guidance, such as checking the connection or trying again.
4. Use Preview in Edit while designing.
5. Publish and deliberately trigger an error to test the result.

### Component Settings

**Preview in Edit** is enabled by default. It controls only the editor preview; published Error content remains hidden until the Form reports a failure.

Error has no other component-specific Inspector settings. Its child components control the message’s content and styling.

### Accessibility

Write a specific message and explain what the visitor can do next. Do not rely on red colour alone, and keep the message close enough to the form that keyboard and screen-reader users can find it.

### Related Components

* [Success](success.md) — Shows confirmation after a successful submission.
* [Form](README.md) — Controls invalid-field colours and delivery.
* [Submit](submit.md) — Provides the clickable submission control.

{% include "../../../.gitbook/includes/common-controls (1).md" %}
