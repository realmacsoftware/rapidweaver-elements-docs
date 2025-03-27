---
description: Apply box shadows rollovers and more.
---

# Effects

Easily enhance the visual appeal of elements in your website by applying effects like box shadow and opacity. These effects can help create depth, highlight key elements, and adjust the transparency of components, giving your site a modern, polished look.

{% embed url="https://youtu.be/IljWfMjwW-Y" %}

### Type

Specify if the component has effects enabled or disabled. The Hover effect works in conjuction with [Transitions](transitions.md).

| Type Properties | Description                                         |
| --------------- | --------------------------------------------------- |
| None            | No effect classes will be applied to the component. |
| Static          | Enable effects.                                     |
| Hover           | Enable Start and End state hover effects.           |

### Hover Over

If you set the `Type` to Hover, you can specify which element should be hovered over to trigger the transition.

| Over Options | Triggers transitions when hovering over…  |
| ------------ | ----------------------------------------- |
| Self         | this element.                             |
| Parent       | the direct parent element.                |
| Container    | any parent Container element.             |
| Grid         | any parent Grid element.                  |
| Flex         | any parent Flex element.                  |
| Custom ID    | the parent with the specified custom ID\* |

#### \*Custom ID Note

When using a Custom ID to trigger a transition, make sure the parent element has a class name in the format `group/{customID}`.

If the parent element is a **Container**, **Grid**, or **Flex** component, you can simply enter the custom ID into the **Advanced → ID** field. Elements will automatically apply the correct class name for you.

However, if you’re using a different component—or have built a custom one—you’ll need to manually ensure the appropriate class name (`group/{customID}`) is applied to that element.

**Note:** You do _not_ need to include the group/ prefix when entering your ID. Just enter the raw ID in the ID field, and Elements will handle the rest.

### Box Shadow

Apply a box shadow to the Component.

### Opacity

Set an opacity for the component.

## Effects UI in Elements

<figure><img src="../../../.gitbook/assets/CleanShot 2024-10-23 at 5 .37.01@2x.png" alt=""><figcaption></figcaption></figure>
