---
description: Perfect for headings and titles.
---

# Text

The Text Component is ideal for headings, taglines, labels, and short text blocks. It gives you precise control over styling, so you can create anything from subtle accents to bold hero text.

You can combine text with background images, gradients, overlays, and utility classes to create more expressive designs. It works well in both simple and complex layouts.

### Getting Started with the Text Component

The following video will teach you the basics on using the Text Component.

{% embed url="https://youtu.be/EVInkOnWHjc" %}

### How to Make Your Text Responsive

The following video shows how to make your text responsive.

{% embed url="https://youtu.be/Vn6saO3ylGg" %}

### Applying Tailwind CSS Classes to Text

This advanced feature lets you apply Tailwind CSS classes to text inside the Text Component.

{% embed url="https://youtu.be/Ql428j-FJ5Y" %}

#### Example Tailwind Classes for Text

Below are a few sample classes featured in the video. To learn more, see the [Tailwind CSS documentation](https://tailwindcss.com/docs/installation).

```css
blur-sm 
hover:blur-sm transition
hover:line-through
inline-block rotate-[2deg]
underline decoration-wavy underline-offset-[10px]
```

### How to Protect Text Content

This is not foolproof. It only discourages casual copying.

Here’s how to add basic text protection to your site:

{% stepper %}
{% step %}
### Add Class to Text Component

Add a `no-copy` class to any Text components you want to protect.

<figure><img src="../../.gitbook/assets/CleanShot 2026-03-14 at 3 .15.38@2x.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Add the CSS Class to the Page

Add the following CSS to the **Edit Page Code** area of the relevant page:

```css
.no-copy {
  user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
}
```

<figure><img src="../../.gitbook/assets/CleanShot 2026-03-14 at 3 .16.23@2x.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Optionally Add JavaScript

You can also add the following JavaScript to the **JS** tab in **Edit Page Code**. This disables right-click on the page.

```javascript
document.addEventListener("contextmenu", e => e.preventDefault());
```

<figure><img src="../../.gitbook/assets/CleanShot 2026-03-14 at 3 .17.54@2x.png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

### Component Settings

{% columns %}
{% column width="50%" %}
#### General

The General section contains the core controls for styling your text. Use these settings to adjust alignment, font, size, weight, spacing, and other properties that apply to the entire text block.

**Tag**

* The Tag helps create a semantic structure, so search engines understand the hierarchy of your content. For example, the main page heading would usually be **Heading 1**, while body text would be **Paragraph**.

**Text Align**

* Align your text left, center, or right. You may also need to set the alignment of the parent item.

**Font**

* Choose a font family. These are managed in [Theme Studio](../theme-studio/).

**Size**

* Choose a text size. These are managed in [Theme Studio](../theme-studio/).
* Text styles include size, line height, letter spacing, and weight. You can override some values inline by choosing **Override**.

**Weight**

* Set the weight of your text.

**Spacing**

* Set the spacing between letters.

**Line Height**

* Set the line height of the text.

**Italic**

* Make the entire text block italic.

**Text Shadow**

* Choose a shadow for your text. These are managed in [Theme Studio](../theme-studio/).

**Case**

* Set the case for the entire text block. The default is **None**.
* None
* Uppercase
* Lowercase
* Capitalise
* Small Caps

**White Space**

`white-space: normal`

* Collapses multiple spaces into one.
* Collapses newlines.
* Allows wrapping.
* This is the default browser behaviour.

`white-space: nowrap`

* Collapses spaces.
* Collapses newlines.
* Prevents wrapping (text stays on one line).

`white-space: pre`

* Preserves spaces exactly as typed.
* Preserves newlines.
* Does not wrap (long lines overflow).
* Behaves like preformatted text.

`white-space: pre-wrap`

* Preserves spaces.
* Preserves newlines.
* Allows wrapping.
* Useful when you want formatting preserved but still fit container width.

`white-space: pre-line`

* Collapses spaces.
* Preserves newlines.
* Allows wrapping.
* Good when line breaks matter but extra spacing should not.

`white-space: break-spaces`

* Preserves spaces.
* Preserves newlines.
* Allows wrapping.
* Spaces can cause line breaks (they become wrap opportunities).
* Trailing spaces are kept and do not collapse.
* Useful for chat UIs or copy/paste content where exact spacing matters.

**Underline**

* Apply a text decoration to the entire block.
* No Underline
* Underline
* Overline
* Line Through
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../../.gitbook/assets/CleanShot 2025-12-12 at 11 .29.53@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}
