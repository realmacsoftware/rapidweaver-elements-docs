---
description: Reveal a second side of content with an interactive 3D card
---

# Card Flip (Paid)

{% hint style="success" %}
Card Flip is available as a **paid product via the Elements Store**. Install the current version of Elements before adding it to a project.
{% endhint %}

Card Flip creates a two-sided card that reveals its back with a smooth horizontal or vertical flip. Each side accepts child components, so a card can contain anything from a short biography to a product summary or call to action.

Cards can flip when clicked, hovered, or on an automatic timer. Optional perspective, tilt, and scale effects add depth while the styling controls keep both sides consistent with your theme.

<a href="elementsapp://storeProduct/com.elementsplatform.cardflippack" class="button primary" data-icon="store">Purchase Card Flip</a>

{% embed url="https://youtu.be/hpbbEuUg9tc" %}

### Features

* **Two component dropzones** — Build the front and back from any Elements components.
* **Click, hover, and automatic triggers** — Choose how visitors reveal the reverse side.
* **Horizontal or vertical movement** — Set the axis and use up to ten complete rotations.
* **Adjustable animation** — Control duration and easing.
* **Optional 3D effects** — Add perspective, pointer-following tilt, and scale.
* **Independent colours** — Style the front and back backgrounds separately.

### Requirements

Before using Card Flip, make sure you have:

* The Card Flip pack installed from the Elements Store.
* Content for both the Front Content and Back Content dropzones.

{% hint style="warning" %}
Hover is not available in the same way on touch devices. Use **Click** when the back of the card contains important information or interactive controls.
{% endhint %}

### Supported Content and File Types

Card Flip supports:

* Any Elements components in the front and back dropzones.
* Text, images, buttons, icons, and other component-based layouts.
* Click, hover, automatic, or manually controlled presentation.

### How to Use Card Flip

You’ll find Card Flip under **Interactive** in the Components list.

1. Drag **Card Flip** onto the page.
2. Add components to the Front Content dropzone.
3. Change **View In Edit** to Back and add the reverse-side content.
4. Choose a Trigger, Direction, Duration, and Easing.
5. Style the two backgrounds, padding, radius, and shadow.
6. Preview the page and test the card with both keyboard and pointer input.

### Component Settings

#### Card Flip

**View In Edit**

Switches between **Front** and **Back** in the editor. It does not set which side visitors see first.

**Trigger**

* **Click** — Flips when the card is clicked or activated from the keyboard.
* **Hover** — Flips while a pointer is over the card.
* **None** — Disables direct click and hover flipping. Use this with Auto Flip when the card should move on a timer.

**Direction**

Choose **Horizontal** or **Vertical** rotation.

**Count**

Sets the number of complete rotations during each flip, from 1 to 10. The default is 1.

**Duration**

Sets the transition time in milliseconds. The default is `600ms`.

**Easing**

Choose **Ease Out**, **Ease In Out**, **Ease In**, or **Linear** to control how the movement accelerates.

**Auto Flip**

Enable automatic flipping and set the **Interval** in seconds. The default interval is 4 seconds and the minimum is 1 second.

#### 3D Effects

**Perspective**

Controls the apparent depth of the animation. Options range from Dramatic to Gentle, with **Balanced** as the default.

**3D Tilt**

When enabled, the card tilts in response to pointer movement. **Intensity** ranges from 5° to 45° and defaults to 15°.

**Scale**

When enabled, the card changes scale during the interaction. **Amount** provides values from 60% to 140%, with 90% as the default.

#### Styling

* **Front / Back** — Set each side’s background colour.
* **Border Radius** — Controls corner rounding for the whole card.
* **Box Shadow** — Adds depth around the card.
* **Padding** — Sets the internal spacing on both sides.

#### Advanced

Use **Classes** to add custom CSS classes and **ID** to assign a unique HTML identifier.

### Accessibility

* Click-triggered cards can be reached and operated from the keyboard. Use Click for content that everyone must be able to reveal.
* Keep visible focus styles on the card and on any links or buttons placed inside it.
* Make the front label explain what the interaction reveals; do not rely on the animation alone.
* Avoid high flip counts, rapid automatic intervals, or strong tilt effects when they are not essential.

### Tips and Best Practices

* **Keep both sides related:** The back should expand on the promise made by the front.
* **Match content height:** Similar amounts of content prevent unexpected card sizing.
* **Use one clear interaction:** Avoid combining Auto Flip with important controls unless visitors have enough time to use them.
* **Test on touch screens:** Confirm that the chosen trigger works without hover.

### Troubleshooting

#### The card does not flip on a phone or tablet

Change Trigger from Hover to Click. Touch devices do not provide a persistent hover state.

#### Child buttons are difficult to use

Use Click thoughtfully, reduce overlapping interactions, and test the focus order. If the card itself and a child control compete for the same click, simplify the card or move the action outside it.

#### The back is difficult to edit

Set **View In Edit** to Back. Switch it to Front when you need to return to the first side.

### Related Components

* [Reveal](../components/reveal.md) — Show content with a simpler reveal interaction.
* [Container](../components/container.md) — Build reusable card layouts without a flip effect.

{% include "../../.gitbook/includes/common-controls.md" %}
