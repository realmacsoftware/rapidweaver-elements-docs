---
description: Set advanced properties for Position, Z-index, Visibility, and more.
---

# Layout

The Layout controls help you manage the overall layout and positioning of elements within a webpage. These controls include controls for handling display properties, positioning, z-index, overflow, visibility, and more.

## General

General layout settings for Position, Z-index, and Inset.

### Position

The Position controls how an element is placed in the document and how it interacts with its surrounding elements. These utilities correspond to standard CSS positioning properties like static, relative, absolute, fixed, and sticky. See [Tailwind CSS Position](https://tailwindcss.com/docs/position) for more details.

<table><thead><tr><th width="194">Position Properties</th><th>Description</th></tr></thead><tbody><tr><td>None</td><td>No position properties are set on the container.</td></tr><tr><td>Static</td><td>The element is positioned according to the normal document flow.</td></tr><tr><td>Relative</td><td>The element is positioned relative to its normal position in the document. You can adjust its position using top, right, bottom, or left properties. The space it originally occupied remains reserved.</td></tr><tr><td>Absolute</td><td>The element is positioned relative to its nearest positioned ancestor (an ancestor that has relative, absolute, or fixed positioning). If no such ancestor exists, the element is positioned relative to the initial containing block (usually the viewport). It is removed from the normal document flow, meaning it does not affect the layout of other elements.</td></tr><tr><td>Fixed</td><td>The element is positioned relative to the viewport, meaning it stays in the same position even when the page is scrolled. Like absolute, it is removed from the document flow and does not affect the positioning of other elements.</td></tr><tr><td>Sticky</td><td>The element is positioned relative until a scroll point is reached, after which it becomes “fixed” and sticks to that position until the scrolling container is out of view. It’s a mix of relative and fixed positioning. You must specify at least one of the top, right, bottom, or left properties for it to stick (e.g. Type > Individual > Top = 5px)</td></tr></tbody></table>

### Z-Index

Controls the stack order of an element on the page. See [Tailwind CSS Z-Index](https://tailwindcss.com/docs/z-index) for more details.

<table><thead><tr><th width="218">Z-Index Properties</th><th>Description</th></tr></thead><tbody><tr><td>None</td><td>No Z-Index properties are set on the container.</td></tr><tr><td>Auto</td><td>Lets the browser automatically determine the Z-index of the container.</td></tr><tr><td>Custom</td><td>Set the Z-index manual for the container,can be a positive or negatiev value (e.g. -50, or 50).</td></tr></tbody></table>

### Type (Inset)

The  Inset property is used to control the positioning of an element relative to its nearest positioned ancestor. [See Tailwind CSS Top / Right / Bottom / Left](https://tailwindcss.com/docs/top-right-bottom-left) for more details.

<table><thead><tr><th width="218">Z-Index Properties</th><th>Description</th></tr></thead><tbody><tr><td>None</td><td>No uniform or individual spacing properties are set on the container.</td></tr><tr><td>Uniform</td><td>Uniform combines the top, right, bottom, and left offset properties into a single option, allowing you to quickly set all four sides at once.</td></tr><tr><td>Individual</td><td>Individual set the top, right, bottom, and left offset properties.</td></tr></tbody></table>

## Advanced

Advanced layout settings for Overflow, Isolation, and Visibility.

### Overflow

Controls how an element handles content that is too large for the container. See [Tailwind CSS Overflow](https://tailwindcss.com/docs/overflow) for more details.

{% embed url="https://youtu.be/rOHL-KScsqc" %}

<table><thead><tr><th width="218">Overflow Properties</th><th>Description</th></tr></thead><tbody><tr><td>None</td><td>No overflow properties are set on the container.</td></tr><tr><td>Visible</td><td>Content that overflows the container will still be visible outside of its bounds.</td></tr><tr><td>Hidden</td><td>Content that exceeds the dimensions of the container is completely hidden (no scrollbars are displayed, and you can’t scroll to see the overflowed content).</td></tr><tr><td>Scroll</td><td>A scrollbar is always shown, regardless of whether the content overflows the container or not. The user can scroll to view the overflowing content.</td></tr><tr><td>Auto</td><td>Scrollbars will automatically appear only if the content overflows the container.</td></tr></tbody></table>

### Isolation

In complex layouts, different elements may interact with each other in ways that are not always predictable, especially when dealing with z-index. Using isolate helps create a new stacking context for an element, effectively “isolating” it from the outside world, preventing unexpected overlaps or stacking behavior. See [Tailwind CSS Isolation](https://tailwindcss.com/docs/isolation) for more details.

<table><thead><tr><th width="203">Isolation Properties</th><th>Description</th></tr></thead><tbody><tr><td>None</td><td>No Isolation properties are set on the container.</td></tr><tr><td>Visible</td><td>Forces an element to create a new stacking context. This isolates the element’s stacking order from the rest of the page, meaning its child elements won’t interfere with other elements on the page, even if they have z-index values.</td></tr><tr><td>Auto</td><td>This is the default setting that lets the browser determine the stacking context without forcing isolation.</td></tr></tbody></table>

### Visibility

Controls the visibility of an element on the page. See [Tailwind CSS Visibility](https://tailwindcss.com/docs/visibility) for more details.

{% embed url="https://youtu.be/Lt9ZGrEG21M" %}

<table><thead><tr><th width="206">Visibility Properties</th><th>Description</th></tr></thead><tbody><tr><td>Auto</td><td>This is the default setting that lets the browser determine the visibility of an element.</td></tr><tr><td>Visible</td><td>When set to visible, the element is fully visible on the page and takes up space in the layout as usual.</td></tr><tr><td>Hidden</td><td>The element is not visible on the page, and the space it occupied will be removed.</td></tr><tr><td>Collapse</td><td>The element is not visible on the page, but it still takes up the same space in the layout as if it were visible. It’s just hidden from view.</td></tr></tbody></table>

## Layout UI in Elements

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-19 at 8 .02.46@2x.png" alt=""><figcaption><p>Component Layout Controls (October 2024)</p></figcaption></figure>

