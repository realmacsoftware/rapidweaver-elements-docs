---
description: Animate components when they enters the viewport
---

# Reveal

The “Reveal” animation component in Elements allows you to add visually engaging animations to your website. As elements come into view, they can “reveal” themselves with smooth, dynamic effects.





### Advanced Usage

By using the data-reveal classes in your [Custom Components](../custom-components.md), you can take advantage of the Animation framework built into Elements.

```html
<div
class="group/reveal block max-w-max" data-reveal-delay="0.1"
data-reveal-exit-animation="lightSpeedRightOut"
data-reveal-start="top bottom"
data-reveal=** data-reveal-distance="208px"
data-reveal-end="top top" 
data-reveal-play="enter-once" 
data-reveal-scrub="false"
data-reveal-easing="power2"
data-reveal-animation="LightSpeedRightIn"
data-reveal-duration="0.5"
data-reveal-degrees="90"
data-reveal-id="reveal-reveal"
>
```

### Animations

Animations in [Custom Components](../custom-components.md) can be set independently on enter and exit, as shown in the sample code.

<pre class="language-textile"><code class="lang-textile">&#x3C;div
class="group/reveal block max-w-max"
data-reveal-delay="0.1"
<strong>data-reveal-animation="LightSpeedRightIn"
</strong>data-reveal-start="top bottom"
data-reveal-exit-animation="lightSpeedRightOut"
data-reveal-end="top top" 
data-reveal-id="reveal-reveal"
>
</code></pre>

The following can be applied to `data-reveal-animation` and `data-reveal-exit-animation` in your [Custom Component](../custom-components.md).

| Reveal Animation   |   |
| ------------------ | - |
| fadeUpIn           |   |
| fadeUpOut          |   |
| fadeDownIn         |   |
| fadeDownOut        |   |
| fadeLeftIn         |   |
| fadeLeftOut        |   |
| fadeRightIn        |   |
| fadeRightOut       |   |
| slideUpIn          |   |
| slideUpOut         |   |
| slideDownIn        |   |
| slideDownOut       |   |
| slideLeftIn        |   |
| slideLeftOut       |   |
| slideRightIn       |   |
| slideRightOut      |   |
| zoomUpIn           |   |
| zoomUpOut          |   |
| zoomDownOut        |   |
| zoomDownIn         |   |
| zoomRightIn        |   |
| zoomRightOut       |   |
| zoomLeftIn         |   |
| zoomLeftOut        |   |
| lightSpeedLeftIn   |   |
| lightSpeedLeftOut  |   |
| lightSpeedRightIn  |   |
| lightSpeedRightOut |   |
| lightSpeedUpIn     |   |
| lightSpeedUpOut    |   |
| lightSpeedDownIn   |   |
| lightSpeedDownOut  |   |
| rotateUpIn         |   |
| rotateDownIn       |   |
| rotateRightIn      |   |
| rotateLeftIn       |   |
| rotateUpOut        |   |
| rotateDownOut      |   |
| rotateRightOut     |   |
| rotateLeftOut      |   |
| bounceInDown       |   |
| swing              |   |











