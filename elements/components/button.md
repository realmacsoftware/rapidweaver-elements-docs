---
description: A fundamental user interface element in web design
---

# Button

Buttons are fundamental user interface elements in web design that enable users to interact with your website. They serve as clickable elements that trigger actions, such as navigating to a new page, or triggering a specific function, like showing a modal window.

{% embed url="https://youtu.be/4zXtboiY8nY" %}

### Common Layout Structure for Buttons

Use a **Flex** component when you want to control how buttons sit next to each other and where they appear inside a layout. The typical structure for this would be:

1. **Container**
2. **Flex** inside the Container
3. **Two or more Buttons** inside the Flex

<figure><img src="../../.gitbook/assets/CleanShot 2026-07-15 at 11 .07.37@2x.png" alt=""><figcaption><p>Center aligned Buttons inside a Flex Component</p></figcaption></figure>

#### Horizontal button alignment

To place buttons side by side:

* Set the **Flex direction** to **Row**.
* Add your **Button** components inside the Flex.

This makes the buttons flow horizontally.

To center the buttons as a group inside the Flex:

* Set **Justify** to **Center**.
* Set **Align Items** to **Center**.

This centers the button row within the Flex container.

By default Button Component margins are usually set to "Auto", so you may need to adjust each button’s margin settings to ensure they are aligned correctly. For centring buttons in a flex:

* Set the button margins to **0** instead of **Auto**.
* Auto margins can override the Flex alignment and push buttons into unexpected positions.
