---
description: Adjust animation curve, duration, and delay for transitions
---

# Transitions

The Transitions settings apply to the Filter, Effect, and Transform sections on the same Component. Transition settings contol the the timing, animation curve and delay when transitioning (or animating) an object between two states.

{% embed url="https://youtu.be/tg2k4ZcFeQg" %}

### Apply to

The Apply to dropdown allows you to specify the values of a component the transition will apply to. In most cases you'll want this set to "All".

* All - Apply a transition to all values.
* None -  Don't apply a transtion (similar to seeing the duration value to 0).
* Most Common - Applies transitions to color, background-color, border-color, text-decoration-color, fill, stroke, opacity, box-shadow, transform, filter, backdrop-filter.
* Colours - Only apply transition to colours.
* Opacity - Only apply transition to the opacity.
* Shadows - Only apply transition to the shadows.
* Transforms - Only apply transition to the Transform values.

### Function

In CSS animations, the terms Linear, Ease In, Ease Out, and Ease-in-out refer to different types of _timing functions_ that control the speed of an animation over time.

* Custom - [See Custom Timing Function (below)](transitions.md#a-note-on-the-custom-timing-function)
* Linear - The animation progresses at a **constant speed** from start to finish.
* Ease In - The animation **starts slowly** and then **speeds up** as it progresses.
* Ease Out - The animation **starts quickly** and then **slows down** as it finishes.
* Ease-in-out - The animation **starts slowly, speeds up**, and then **slows down** again before finishing.

#### Custom Timing Functions

The x1, y1, x2, and y2 values used to create custom timing functions using a cubic-bezier() curve for animations.

The cubic-bezier curve essentially determines the rate of change over time of the animation. It allows you to create custom easing effects that can behave in ways that predefined ones like linear, ease-in, ease-out, or ease-in-out cannot.

**x1, x2:** Control the horizontal axis, which represents time. These values must be between 0 and 1, where 0 is the start of the animation and 1 is the end.

**y1, y2:** Control the vertical axis, which represents the progress of the animation (i.e., how far along the element is in its transformation or movement). These values can go below 0 or above 1 to create exaggerated effects.

#### Example Animation Curves

The following animation starts very quickly, with almost no easing at the beginning, very fast through the middle section and ends abruptly. These values are the default values for the custom timing control.

```
0.95,0.05,0.795,0.035
```

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-17 at 10 .31.23.gif" alt=""><figcaption></figcaption></figure>

The following animation accelerates towards the end point, overshoots the final position, and comes back to settle into its final state.

```
0.21,1,1,1.53
```

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-17 at 10 .28.15.gif" alt=""><figcaption></figcaption></figure>

There are tools online like [Cubic-Bezier.com](https://cubic-bezier.com) that let you visually manipulate and experiment with the cubic-bezier function to create custom easing effects, where you can adjust the control points and immediately see the animation effect on a graph.

### Duration

Set the duration for the transition animation in milliseconds, for example setting a value of 500, would result in the transition taking 0.5 seconds to complete. Setting the value to 1,000 would make the transition taking 1 second to complete.

### Delay

Set the delay of the transition start in milliseconds, for example setting a value of 500, would result in a delay of 0.5 seconds before the animation will start. Setting the value to 1,000 would set a delay of 1 second before the animation starts.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-17 at 9 .52.22@2x.png" alt=""><figcaption><p>Transitions UI</p></figcaption></figure>

