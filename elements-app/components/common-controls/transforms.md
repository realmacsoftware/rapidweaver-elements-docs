---
description: Apply effects like rotate, scale, skew, and more.
---

# Transforms

Transforms in Elements allow you to manipulate the position, size, and orientation of components all without writing a line of code. Transforms are a powerful way to apply effects like rotating, scaling, translating (moving), and skewing elements, making it easy to add dynamic and interactive visual effects to your design.

You can also use transforms to create hover or focus effects that make elements feel more interactive and responsive.

{% embed url="https://youtu.be/BFDklORPBHA" %}

### Type

Specify if the component has transforms enabled or disabled. The Hover effect works in conjuction with [Transitions](transitions.md).

| Type Properties | Description                                         |
| --------------- | --------------------------------------------------- |
| None            | No effect classes will be applied to the component. |
| Static          | Enable effects.                                     |
| Hover           | Enable Start and End state hover effects.           |

### Custom ID's for Hover

The component must be nested somewhere inside a component that has the custom ID applied, and the custom id class needs to be formatted with the group modifier, like so: `group/parent-component-id`.

### Transforms

* Origin - Set the origin of the transform.
* Scale - Changes the size of an element by percent.
* Rotate - Rotates an element by a specified degree, supports positive and negative values.
* Translate - Moves an element along the X or Y axis, supports positive and negative values.
* Skew - Skews an element along the X or Y axis, supports positive and negative values.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-24 at 12 .08.31@2x.png" alt=""><figcaption></figcaption></figure>
