---
description: Create linked groups of components that update throughout your website
icon: globe
---

# Globals

Globals give you the power to create reusable linked (and customisable) groups of components to maintain a consistent design language across your entire site.

You can reuse global template blocks across your site so you only need update the content in one place and have it automagically mirrored in all other instances of that global. For example, this can be very  useful for global header and footer sections.

{% hint style="warning" %}
Templates are very similar to Globals, but there's one important difference: **Templates are single use and not linked**. Where's Globals remain linked and are perfect for making changes across your entire site, perfect for shared menus and footers. [Learn more about Templates here](templates.md).
{% endhint %}

{% embed url="https://youtu.be/wMl2M8YstkE" %}

You can take Globals even further by overriding content and design aspects on an individual instance. You might have a banner that you want to use on every page of your site and you'd like the design to be consistent. You can use the override feature to customise the text and background image on each instance. You can even override the design settings on certain instances.

{% hint style="info" %}
Global Templates help ensure the design for you website is modular, reusable, and consistent.
{% endhint %}

Once you learn how to use the power of globals you'll wonder how you ever built wesbites without them.

### Creating a Global

There are a number of ways to turn a group of Elements into a Global. Right-click an element in the Editor or Node Browser and select "Convert to Global".

### Unlinking a Globals

To unlink a group of Elements on a page, right-click on the Global in the Node Browser and choose "Unlink from Global".

### Globals inside Globals

When working with Elements, you can nest different Globals within each other to create complex structures. However, it's important to note that you cannot nest the same Global within itself. This restriction is in place to prevent potential issues such as infinite loops, system errors, or a rip in the time-space continuum.
