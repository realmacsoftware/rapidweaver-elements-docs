---
description: Set the Width and Height for elements.
---

# Sizing

The sizing option provides options for setting fixed widths, percentage-based widths, viewport-based widths, and even fractional widths to ensure flexibility and precision in responsive design.

{% embed url="https://youtu.be/cCSxBM194SQ" %}

### Width

The width setting offers a comprehensive range of options that make it easy to control the width of elements in your design.

<table><thead><tr><th width="194">Position Properties</th><th>Description</th></tr></thead><tbody><tr><td>Auto</td><td>No position properties are set on the element, the parent element and browser handles the width of the element.</td></tr><tr><td>Full</td><td>The element will take up the full width of the parent element.</td></tr><tr><td>Screen</td><td>The element will take up the full width of the viewport, e.g. 100vw (full viewport width).</td></tr><tr><td>Breakpoint</td><td>The element width will be to set to the Breakpoint classes setup in the Theme Studio.</td></tr><tr><td>Theme Spacing</td><td>Choose from the pre-defined size classes set in the Theme Studio. You can also override the pre-defined classes and use <a href="/broken/pages/ocNrfx1gyJHmVYZMYP0k">Custom CSS Values</a>.</td></tr></tbody></table>

### Height

The height setting offers a comprehensive range of options that make it easy to control the height of elements in your design.

<table><thead><tr><th width="194">Position Properties</th><th>Description</th></tr></thead><tbody><tr><td>Auto</td><td>No position properties are set on the element, the parent element and browser handles the height of the element.</td></tr><tr><td>Full</td><td>The element will take up the full height of the parent element.</td></tr><tr><td>Screen</td><td>The element will take up the full hight of the viewport, e.g. 100vh (full viewport height).</td></tr><tr><td>Theme Spacing</td><td>Choose from the pre-defined size classes set in the Theme Studio. You can also override the pre-defined classes and use <a href="/broken/pages/ocNrfx1gyJHmVYZMYP0k">Custom CSS Values</a>.</td></tr></tbody></table>

### Min & Max Settings

In Elements the min-width and max-width settings provide control over the minimum and maximum width of elements, allowing you to set constraints on how wide an element can grow or shrink. These settings are especially useful for responsive design, as they help maintain readability and layout consistency across different screen sizes.

#### Why Use Min-Width and Max-Width?

1\. Content Readability: Setting maximum widths prevents text from stretching too wide, which enhances readability, especially on larger screens.

2\. Responsive Design: Min and max-widths help maintain an adaptable layout by controlling how elements respond to different screen sizes.

3\. Layout Constraints: Min-widths prevent elements from collapsing too small, while max-widths keep elements from overflowing their containers, ensuring a balanced and visually consistent design.

Use min-width and max-width settings when you need control over element sizes to ensure responsive, readable, and user-friendly layouts across various screen sizes.

### Using Custom CSS Values

A lot of Components support a “custom sizing” option for you to specify the exact size of an element, this can be things like width, height, and placement.

When adding a value into the custom size box, it’s useful to remember that anything native css supports, Elements supports! So values like vh, px, rem, %, and [css maths 2](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions/Using_CSS_math_functions) should all work as expected.

Here's some examples:

* 250px - Make the width (or hight) 250px wide.
* calc(100vw-20px) - 100% viewport width - 20px.
* 100vw - 100% of the viewport width.
* 80vh - 80% of the viewport height.

## Sizing UI in Elements

<figure><img src="../../.gitbook/assets/CleanShot 2024-10-28 at 11 .51.11@2x.png" alt=""><figcaption></figcaption></figure>
