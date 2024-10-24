---
description: Automatic colour switching based on the users system settings
---

# Dark Mode

With dark mode now a prominent feature in many operating systems, it’s increasingly common to create a dark version of your website alongside the default design.

Elements supports automatic switching between light and dark mode. This approach enables automatic theme switching based on the user’s system (or browser) settings, ensuring websites adapts seamlessly to both light and dark modes.

### Choosing Background and Text Colours

For Light and Dark mode to work seamlessly we recommend basing your websites on the following three colours, **Brand**, **Surface**, and **Text**.

* For **Elements** like Buttons, Colour Fill on Icons, Dividers, we recommend using **Brand Colour** from the Theme Studio.
* For **Background Colours** we recommend using the **Surface colour** from the Theme Studio.
* For **Text Colours** we recommend using the **Text colour** from the Theme Studio.

### Changing Colours based on Mode

Every colour in Elements supports Dark and Light Mode, this means you can change the colour of text, backgrounds, buttons, borders, and more, all based on the users system settings.

By default when you set a colour it's set for Light Mode. To set an alternative colour for Dark mode, you need to press the Dark/Light Mode toggle button at the top of the editor.

### Hide and Show Components based on Mode

If you'd like to hide and show other elements (including images) based on the users system settings you can use the following classes.

To **hide Components in Dark mode** use the following class:

`dark:hidden`

To **hide Components in Light Mode** use the following classes:

`hidden dark:block`

### Dev Diary Videos for Dark Mode

The following video will show you how to set Colours for  Dark and Light mode in Elements. The video was recorded with a development version of Elements so the feature(s) available now may differ slightly to those in the video.

{% embed url="https://youtu.be/dZkGtd1sHPc" %}
