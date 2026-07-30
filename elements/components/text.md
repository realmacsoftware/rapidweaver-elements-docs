---
description: Create headings, paragraphs, labels, and short text blocks
---

# Text

The Text component creates editable headings, paragraphs, taglines, labels, and other short text. It provides responsive typography, solid or gradient text colour, link states, decoration, effects, and semantic HTML tags.

### How to Use Text

You’ll find Text under **Content** in the Components list.

1. Drag **Text** onto the page.
2. Edit the text directly on the page.
3. Choose the correct semantic Tag.
4. Set alignment, font, size, weight, spacing, line height, and colour.
5. Configure link or hover states where required.

{% embed url="https://youtu.be/EVInkOnWHjc" %}

### Responsive Text

Text size and many other controls can change by breakpoint.

{% embed url="https://youtu.be/Vn6saO3ylGg" %}

### Component Settings

#### General

**Tag** controls the rendered HTML and defaults to Paragraph. Options are Paragraph, Heading 1–6, Span, Div, or Custom. Custom reveals a Custom Tag field that defaults to `div`.

The tag affects semantics and SEO rather than visual appearance. Use one Heading 1 for the page’s main subject, then maintain a logical heading order.

**Text Align** offers Left, Centre, Right, or Justify and defaults to Left.

**Font** defaults to Body and **Size** to Base.

**Weight** ranges from Thin 100 to Black 900 and defaults to 400.

**Spacing** offers Tighter through Widest and defaults to Normal.

**Line Height** offers None, Tight, Snug, Normal, Relaxed, or Loose and defaults to Normal.

**Italic** is off and **Text Shadow** defaults to None.

**Case** offers None, Uppercase, Lowercase, Capitalise, or Small Caps and defaults to None.

**Whitespace**

* **None** — Applies no extra whitespace class. This is the default.
* **Normal** — Collapses spaces and allows wrapping.
* **Nowrap** — Prevents wrapping.
* **Pre** — Preserves spaces and line breaks without wrapping.
* **Pre Line** — Collapses spaces but preserves line breaks.
* **Pre Wrap** — Preserves spaces and line breaks while allowing wrapping.
* **Break Spaces** — Preserves spaces and lets them become wrapping opportunities.

**Underline** offers No Underline, Underline, Overline, or Line Through. When enabled, Style offers Solid, Double, Dotted, Dashed, or Wavy. Underline also reveals Offset, which defaults to 1 pixel. Decoration Color defaults to Text 100 at 100% opacity.

<figure><img src="../../.gitbook/assets/CleanShot 2025-12-12 at 11 .29.53@2x.png" alt="Text General settings for semantic tag, alignment, font, size, weight, spacing, line height, and decoration"><figcaption><p>General settings control the Text component’s semantics and typography.</p></figcaption></figure>

#### Color

**Type** can be Static or Hover and defaults to Static. Hover lets Self, Parent, Container, Grid, Flex, or a Custom ID trigger the colour change, then provides Start and End states.

**Style** can be Color, Image, or Gradient and defaults to Color.

Solid text defaults to Text 50 at 100% opacity. The hover End colour defaults to Text 200.

Gradient text can be Linear, Radial, or Conic. Set direction or position, interpolation, From and To colours, opacity, and stop positions. **Add Via** inserts an optional middle colour.

Image text uses a resource with Position, Size, Repeat, and Fetch Priority controls.

#### Links

Use **State** to style Default, Hover, and Visited links independently.

Each state provides Color, Font Weight, and Underline. Default links use Brand 500; Hover and Visited use Brand 800. Weight defaults to 400.

### Applying Tailwind CSS Classes

Advanced classes can create one-off effects inside a Text component.

{% embed url="https://youtu.be/Ql428j-FJ5Y" %}

Examples from the video:

```css
blur-sm
hover:blur-sm transition
hover:line-through
inline-block rotate-[2deg]
underline decoration-wavy underline-offset-[10px]
```

See the [Tailwind CSS documentation](https://tailwindcss.com/docs/) for available utilities.

### Discouraging Casual Text Copying

This does not securely protect published text; it only discourages casual selection.

1. Add a `no-copy` class to the Text component.
2. Add this CSS in **Edit Page Code → CSS**:

<figure><img src="../../.gitbook/assets/CleanShot 2026-03-14 at 3 .15.38@2x.png" alt="A Text component with no-copy entered in its Classes field"><figcaption><p>Add the no-copy class to each Text component you want to affect.</p></figcaption></figure>

```css
.no-copy {
  user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
}
```

<figure><img src="../../.gitbook/assets/CleanShot 2026-03-14 at 3 .16.23@2x.png" alt="Page CSS containing a no-copy class that disables text selection"><figcaption><p>The no-copy class added to the page CSS.</p></figcaption></figure>

Optionally add this in **Edit Page Code → JavaScript** to disable the page’s context menu:

```javascript
document.addEventListener("contextmenu", e => e.preventDefault());
```

<figure><img src="../../.gitbook/assets/CleanShot 2026-03-14 at 3 .17.54@2x.png" alt="Page JavaScript that prevents the browser context menu from opening"><figcaption><p>Optional JavaScript that disables right-click on the page.</p></figcaption></figure>

### Accessibility

Choose semantic tags for meaning, preserve a logical heading hierarchy, and keep text readable when responsive sizes, gradients, effects, or whitespace settings are applied.

### Related Components

* [Typography](typography.md) — Styles long-form structured content.
* [Markdown](markdown.md) — Writes formatted content using Markdown syntax.
* [Button](button.md) — Creates a prominent linked action.

{% include "../../.gitbook/includes/common-controls.md" %}
