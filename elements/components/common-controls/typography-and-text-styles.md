---
description: Control fonts, text size, spacing, decoration, colour, and semantic wrappers
---

# Typography & Text Styles

Text-style controls use Theme Studio fonts and text styles while allowing component-level alignment, weight, spacing, line height, case, decoration, and state changes.

### Theme Typography

Markdown and Typography components can apply a Theme Studio Typography preset to an entire structured block.

**Style** defaults to Article.

**Tag** is not responsive and defaults to Article. Options are Article, Section, Aside, Main Content, Header, Footer, Div, and Span.

The tag changes document meaning, not appearance. Use Main Content only once on a page.

### Alignment

Text alignment is responsive where provided.

* Text offers Left, Centre, Right, and Justify, defaulting to Left.
* Button labels offer Start, Centre, and End, defaulting to Centre.
* Input text offers Start, Centre, and End, defaulting to Start.

### Font and Size

**Font** or **Family** defaults to Body.

**Size** defaults to Base.

Both use Theme Studio values and can be changed responsively.

### Font Settings

Common defaults are:

* **Weight** — 400/Normal.
* **Spacing** or **Letter Spacing** — Normal.
* **Line Height** — Normal.
* **Case** — None.
* **Italic** — Off.
* **Text Shadow** — None.

Weight options run from Thin 100 to Black 900. Case options include Uppercase, Lowercase, and Capitalise; general Text also supports Small Caps.

### Whitespace

Text and List styles can provide:

* **None** — Applies no whitespace class. This is the default.
* **Normal** — Collapses spaces and allows wrapping.
* **Nowrap** — Prevents wrapping.
* **Pre** — Preserves spaces and line breaks without wrapping.
* **Pre Line** — Collapses spaces but preserves line breaks.
* **Pre Wrap** — Preserves spaces and line breaks and allows wrapping.
* **Break Spaces** — Preserves spaces and lets them form wrapping opportunities.

### Underline and Decoration

The general Text style defaults to No Underline. Options are Underline, Overline, and Line Through.

When a decoration is selected:

* **Style** defaults to Solid and can be Double, Dotted, Dashed, or Wavy.
* **Offset** appears for Underline, ranges from 0–30 pixels, and defaults to 1 pixel.
* **Color** defaults to Text 100.
* **Opacity** ranges from 0–100% and defaults to 100%.

Button and input variants provide a simpler Underline switch, which is off by default.

### Colour and States

The available colour controls depend on the component.

* General input text defaults to Text 50 at 100% opacity.
* Button text defaults to Surface 50 at 100% opacity and provides Normal and Hover states.
* Text links provide Default, Hover, and Visited states in the Text component.

Use a [Transition](transitions.md) when a Hover text state should animate.

### Semantic Tags

Some components provide their semantic Tag in the text group:

* Text defaults to Paragraph and offers Paragraph, Heading 1–6, Span, Div, and Custom.
* Custom Text tags reveal a field defaulting to `div`.
* Markdown and Typography use the block-level tags listed under Theme Typography.

Choose tags for structure and accessibility. Keep heading levels in a logical order and do not choose a heading merely to obtain its visual size.

### Responsive Typography

Set the Base font and size first. Add breakpoint overrides only when the type scale, alignment, or spacing needs to change. Check that long words, enlarged text, and translated content still wrap without clipping.
