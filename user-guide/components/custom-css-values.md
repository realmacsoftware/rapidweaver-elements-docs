# Custom CSS Values

A lot of Elements support a “custom sizing” option for you to specify the exact size of an element, this can be things like width, height, and placement.

When adding a value into the custom size box, it’s useful to remember that anything native css supports, Elements supports! So values like vh, px, rem, %, and [css maths 2](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS\_Functions/Using\_CSS\_math\_functions) should all work as expected.

Here's some examples:

* 250px - Make the width (or hight) 250px wide.
* calc(100vw-20px) - 100% viewport width - 20px.
* 100vw - 100% of the viewport width.
* 80vh - 80% of the viewport height.

