---
description: Perfect for headings and titles.
---

# Text

The Text Component is an ideal choice for a wide range of text elements, from headings and taglines to smaller text areas. It provides flexibility for styling text to suit various design needs, making it perfect for creating visually impactful headings, standout taglines, and highlighted phrases.

With the Text Component, you can easily create **bold, eye-catching** headings enhanced by background images, gradients, or color overlays, adding depth and style to your design. The component’s versatility means it works seamlessly in both minimal and complex layouts, allowing you to design text elements that grab attention without overpowering your overall look.&#x20;

Whether you’re looking to create subtle text accents or prominent, styled headers, the Text Component has you covered.

### Gettings Started with Text Compotnent

The following video will teach you the basics on using the Text Component.

{% embed url="https://youtu.be/EVInkOnWHjc" %}

### How to Make Your Text Responsive

The following video will show you how to make your text resposive.

{% embed url="https://youtu.be/Vn6saO3ylGg" %}

### Applying Tailwind CSS Classes to Text

This is an advanced feature that allows you to apply Tailwind CSS Classes to any of your text in the Text Component.

{% embed url="https://youtu.be/Ql428j-FJ5Y" %}

#### Example Tailwind Classes for Text

Below we have included a few sample classes that were featured int he video. To learn more you can [browse the Tailwind CSS Docs](https://tailwindcss.com/docs/installation).

```css
blur-sm 

hover:blur-sm transition

hover:line-through

inline-block rotate-[2deg]

underline decoration-wavy underline-offset-[10px]
```

### Component Settings

{% columns %}
{% column width="50%" %}
#### General

The General section contains the core controls for styling your text. Use these settings to adjust alignment, font, size, weight, spacing, and other properties that apply to the entire text block.

**Tag**

* The Tag helps create a semantic structure so search engines understand the hierarchy and relationship of your content. For example, the main heading on the page choose would be "Heading 1", your body text would be set "Paragraph".

**Text Align**

* Align your text, left, center and right. You may need to also set the alignment of the parent item to get the desired alignment.

**Font**

* Choose a font family, these are managed by the [Theme Studio](../elements/theme-studio/).

**Size**

Choose a text size, these are managed by the [Theme Studio](../elements/theme-studio/).

* Text styles include size, line height, letter spacing, and weight. You can override some of these settings inline by choosing the "Override" option.

**Weight**

* Set the weight of your text.

**Spacing**

* Set the spacing between letters.

**Line Height**

* Set the line height of the text.

**Italic**

* Make the entire text black italic.

**Text Shadow**

Choose a shadow for your text, these are managed by the [Theme Studio](../elements/theme-studio/).

**Case**

You can set the case for the entire block of text. by default this is set to None.

* None
* Uppercase
* Lowercase
* Capitalise
* Small Caps

**White Space**

white-space: normal

* Collapses multiple spaces into one.
* Collapses newlines.
* Allows wrapping.
* This is the default browser behaviour.

white-space: nowrap

* Collapses spaces.
* Collapses newlines.
* Prevents wrapping (text stays on one line).

white-space: pre

* Preserves spaces exactly as typed.
* Preserves newlines.
* Does not wrap (long lines overflow).
* Behaves like the tag.

white-space: pre-wrap

* Preserves spaces.
* Preserves newlines.
* Allows wrapping.
* Useful when you want formatting preserved but still fit container width.

white-space: pre-line

* Collapses spaces.
* Preserves newlines.
* Allows wrapping.
* Good when line breaks matter but extra spacing should not.

white-space: break-spaces

* Preserves spaces.
* Preserves newlines.
* Allows wrapping.
* Spaces can cause line breaks (they become wrap opportunities).
* Trailing spaces are kept and do not collapse.
* Useful for chat UIs or copy/paste content where exact spacing matters.

**Underline**

Apply an underline to the entire text block.

* No Underline
* Underline
* Overline
* Line Through
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../.gitbook/assets/CleanShot 2025-12-12 at 11 .29.53@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

