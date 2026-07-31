# Design a Decorative Dividers

In this video we show you how to design a decorative divider using just the flex and divider components.

{% embed url="https://www.youtube.com/watch?v=GpKCgikpUvQ" %}

### Building a Decorative Divider in Elements

The decorative divider is built entirely from standard Elements components, no custom component is required.

* Container
  * &#x20;Flex
    * Divider
    * Divider or SVG
    * Divider

#### How it works

1. Add a Container to control the divider’s overall width and vertical spacing.
2. Place a Flex inside it.
3. Set the Flex direction to Row, alignment to Centre, width to Full, and wrapping to No Wrap.
4. Add three Divider elements to the Flex.
5. Use the first and third Dividers as the horizontal rules. Give them the same theme-backed background colour and leave their borders disabled.
6. For the centre Divider:
   * Remove its background.
   * Enable a solid border.
   * Use the same colour as the outer rules.
   * Apply the Full border-radius token to create the rounded medallion.

The two outside Dividers expand into the available space, while the centrepiece retains its natural size. This creates two balanced rules without requiring fixed widths.

#### Using an SVG centrepiece

For an illustrated variation, replace the middle Divider with an SVG element. Select an SVG resource, give it a fixed theme width, and apply the same theme colour used by the rules.

The SVG file should not contain a hard-coded fill colour, allowing Elements to apply the selected theme colour.

#### Responsive behaviour

The Flex remains on one line while the two rules automatically shorten on narrower screens. Keep the centrepiece relatively small so the rules remain visible on mobile devices.

#### Accessibility

Because the divider is purely decorative, its outer Container should normally render as a div, rather than a header or another landmark element.
