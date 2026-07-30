---
description: Display focused content in an overlay above the current page
---

# Modal

The Modal component displays content above the current page with a configurable backdrop. It is useful for forms, announcements, image or video presentations, sign-up prompts, and other content that needs temporary focus.

A Modal has separate trigger and content drop zones. Add a Modal Close component anywhere inside the content to give visitors an explicit way to dismiss it.

{% embed url="https://youtu.be/Ye1Eyfyh3DE?si=LQiriRcrp0urI0VU" %}

### How to Use Modal

You’ll find Modal and Modal Close under **Interactive** in the Components list.

1. Drag **Modal** onto the page.
2. Add a Button, Image, or other suitable trigger to its trigger drop zone.
3. Enable **Settings → Show** while building the modal content.
4. Add content to the modal and include a **Modal Close** component.
5. Configure placement, transition, and overlay.
6. Disable Show and preview the open and close behaviour in a browser.

### Component Settings

#### Settings

**Show** displays the modal in Edit mode. It is off by default and does not force the published modal to remain open.

**Auto Open**

* **Never** — Opens only from its trigger. This is the default.
* **Page Load** — Opens when the page loads.
* **After Delay** — Opens after the specified number of Seconds.
* **Exit Intent** — Opens when pointer movement suggests the visitor is leaving the page.

**Seconds** appears for After Delay and defaults to 0.

#### Transition

**Style** offers Fade, Zoom, Slide Left, Slide Right, Slide Up, or Slide Down. Fade is the default.

**Duration** sets the animation length in milliseconds and defaults to 300.

#### Trigger

**Cursor** controls the pointer shown over the trigger: Default, Pointer, Help, or Zoom In. Default is selected initially.

#### Content

**Horizontal** places modal content at Start, Centre, or End and defaults to Centre.

**Vertical** uses the same positions and also defaults to Centre.

#### Overlay

**Color** defaults to Surface 50 and **Opacity** to 15%. **Blur** softens the page behind the modal.

#### Modal Close

The Modal Close component closes its parent Modal when activated. Its **Cursor** can be Default, Pointer, or Zoom Out and defaults to Default.

You can add more than one Modal Close component—for example, an icon in the top-right and a Cancel button below a form.

### Accessibility

Provide an obvious close control, keep it keyboard accessible, and use a clear heading inside the modal. Do not open non-essential modals automatically on every visit.

### Tips and Best Practices

* **Use Show only while editing:** Disable it before testing the real interaction.
* **Keep content focused:** A modal should have one clear purpose.
* **Test small screens:** Ensure the content fits and the close control remains visible.

### Related Components

* [Button](button.md) — Creates a clear modal trigger or close action.
* [Dropdown](dropdown.md) — Better suited to compact contextual content.
* [Image](image.md) — Includes a simpler built-in image lightbox.
