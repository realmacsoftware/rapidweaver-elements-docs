---
description: Animate components when they enters the viewport
---

# Reveal

The “Reveal” animation component in Elements allows you to add visually engaging animations to your website. As elements come into view, they can “reveal” themselves with smooth, dynamic effects.

{% embed url="https://www.youtube.com/watch?v=7zZiIZtXf9c" %}

### Advanced Usage

By using the `data-reveal-*` attributes in your [Custom Components](../custom-components.md), you can take advantage of the Animation framework built into Elements.

As a minimum you can add `data-reveal` to any DOM element to apply a default animation as the element enters the viewport. If you would like to customise the animation, the following data attributes are available.

| Attribue                   | Type           | Notes                                                                         |
| -------------------------- | -------------- | ----------------------------------------------------------------------------- |
| data-reveal                | String \| null | Does not require a value.                                                     |
| data-reveal-scrub          | Boolean        | Enable scrubbing.                                                             |
| data-reveal-animation      | String         | See [available animations](reveal.md#available-animations)                    |
| data-reveal-exit-animation | String         | See [available animations](reveal.md#available-animations)                    |
| data-reveal-distance       | CSS Value      | 200px, 75%, 33vh.                                                             |
| data-reveal-degrees        | Number         | 90, -45, 312.                                                                 |
| data-reveal-play           | String         | See [available play methods](reveal.md#available-play-methods).               |
| data-reveal-start          | String         | See [GSAP docs](https://gsap.com/docs/v3/Plugins/ScrollTrigger/?page=1#start) |
| data-reveal-end            | String         | See [GSAP docs](https://gsap.com/docs/v3/Plugins/ScrollTrigger/?page=1#end)   |
| data-reveal-easing         | String         | See [GSAP docs](https://gsap.com/docs/v3/Eases)                               |
| data-reveal-duration       | Number         | In seconds                                                                    |
| data-reveal-delay          | Number         | In seconds                                                                    |
| data-reveal-id             | String         | Optional ID, used to identify debug markers.                                  |
| data-reveal-debug          | Boolean        | Enables debug markers                                                         |

### Available Play Methods

Elements allows you to define when the animation should be triggered. You can use any of these values when setting the `data-reveal-play`attribute.

| Name            | Value          | Notes                                                      |
| --------------- | -------------- | ---------------------------------------------------------- |
| Once on enter   | `enter-once`   | One time animation when first entering the viewport        |
| Always on enter | `enter-always` | Plays every time the elements enters the viewport          |
| Enter and exit  | `enter-exit`   | Plays every time the element enters and exits the viewport |

### Animations

Animations in [Custom Components](../custom-components.md) can be set independently on enter and exit, as shown in the sample code.

<pre class="language-textile"><code class="lang-textile">&#x3C;div
    data-reveal
<strong>    data-reveal-animation="lightSpeedRightIn"
</strong><strong>    data-reveal-exit-animation="fadeUpOut"
</strong>>
</code></pre>

We offer five types of animations to enhance your user interface:

• Fade

• Slide

• Zoom

• Light Speed

• Rotate

Each animation supports all four directions (_Up_, _Down_, _Left_, _Right_) and can be triggered for both “In” and “Out” events.

Our animation naming convention is straightforward, following this structure:

`{animationName}{Direction}{Event}`

For example:

• `fadeUpIn` for a fade-in effect moving upwards.

• `zoomLeftOut` for a zoom-out effect moving to the left.

This flexible system ensures that you can seamlessly integrate animations tailored to your design needs.

### Available Animations

| Animation Name     | Description     |
| ------------------ | --------------- |
| fadeUpIn           | Fade Up and In  |
| fadeUpOut          | Fade Up and Out |
| fadeDownIn         | ...             |
| fadeDownOut        |                 |
| fadeLeftIn         |                 |
| fadeLeftOut        |                 |
| fadeRightIn        |                 |
| fadeRightOut       |                 |
| slideUpIn          |                 |
| slideUpOut         |                 |
| slideDownIn        |                 |
| slideDownOut       |                 |
| slideLeftIn        |                 |
| slideLeftOut       |                 |
| slideRightIn       |                 |
| slideRightOut      |                 |
| zoomUpIn           |                 |
| zoomUpOut          |                 |
| zoomDownIn         |                 |
| zoomDownOut        |                 |
| zoomRightIn        |                 |
| zoomRightOut       |                 |
| zoomLeftIn         |                 |
| zoomLeftOut        |                 |
| lightSpeedLeftIn   |                 |
| lightSpeedLeftOut  |                 |
| lightSpeedRightIn  |                 |
| lightSpeedRightOut |                 |
| lightSpeedUpIn     |                 |
| lightSpeedUpOut    |                 |
| lightSpeedDownIn   |                 |
| lightSpeedDownOut  |                 |
| rotateUpIn         |                 |
| rotateDownIn       |                 |
| rotateRightIn      |                 |
| rotateLeftIn       |                 |
| rotateUpOut        |                 |
| rotateDownOut      |                 |
| rotateRightOut     |                 |
| rotateLeftOut      |                 |

### Full Example

```html
<div
    data-reveal
    data-reveal-scrub="false"
    data-reveal-animation="fadeUpIn"
    data-reveal-exit-animation="fadeUpOut"
    data-reveal-distance="200px"
    data-reveal-degrees="90"
    data-reveal-play="enter-exit"
    data-reveal-start="top bottom"
    data-reveal-end="top top" 
    data-reveal-easing="power1.out"
    data-reveal-duration="0.5"
    data-reveal-delay="0"
    data-reveal-id="optional-reveal-id"
    data-reveal-debug="false"
>
```









