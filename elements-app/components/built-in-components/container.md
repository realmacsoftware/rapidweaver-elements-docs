# Container

The Container Element serves as a wrapper or holder for other elements. It is commonly used to group and organise related content. The Container Element can be used to apply spacing or create space around elements.

{% hint style="info" %}
The container width can be set up globally for each breakpoint in the [Screens area](../../theme-studio/screens.md) of the Theme Studio.
{% endhint %}

### Layout Group

#### Margin

The Margin allows you to set the margin on all sides of the container. You can adjust the left and right margins to set the spacing as follows:

* **Align Center**, set the let and right margin to "Auto"
* **Align Left**, set the left and right margin to "0"
* **Align Right**, set the left margin to "0" and the right margin to "auto"

#### Padding

Apply padding independently to each side of the element.

### Advanced Group

#### Visible

Visually show and hide the element. Please note the element will still be visible in the html, but not visible on the page.

#### CSS Classes

Add custom (and Tailwind) classes directly to this element. For example, we can apply a blur to everything within the container by writing `blur-sm` into the CSS Classes field. See the [Tailwind blur docs](https://tailwindcss.com/docs/blur) for available classes.

You can browse all the available Tailwind classes over in the [Tailwind CSS documentation](https://tailwindcss.com/docs/).

#### Clip Content

Clip content that overflows this Element.



