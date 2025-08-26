---
description: Learn more about how the Elements design system works.
icon: pen-ruler
---

# Design System

If you're just starting out with Elements it's important to take the time to learn the difference between Components, Templates, and Global Templates.

It's also worth noting that Elements is a Mobile first design system, based on Tailwind CSS. You can learn about all of this and more below.&#x20;

{% hint style="info" %}
If you have any questions, please [visit the forum](https://forums.realmacsoftware.com), we're always around to help!
{% endhint %}

### Components

The core components inside elements represent the basic building blocks of a webpage; they are at the foundation of your page design. They include things like containers, grids, headings, text, and buttons. They are singular items, like Lego bricks.

Some of the more advanced components go beyond the basics; these include things like menus and galleries.

### Templates

Templates are groups of Components that have been put togther to create a design or layout. Once a template is dropped into your page you can customise it however you like and it won't affect the original.

The core pack inside of Elements includes a selection of useful layouts for everyday web design, including menus, hero banners, layouts, forms, and more.

You can learn more about [Templates and how they differ to Global Templates here](../editor/templates.md).

### Global Templates

[Global Templates](design-system.md#global-templates) (or Globals as they are often called) are user created groups of components. Globals can help maintain a consistent design language across your entire site.

You can reuse global blocks across your site so you only need to update the content in one place and have it automagically mirrored to all other instances of that global. For example, this can be very useful for header and footer sections.

You can take Globals even further by overriding content and design aspects on an individual instance. For example, you might have a banner that you want to use on every page of your site, and you'd like the design to be consistent. You can use the override feature to customise the text and background image on each instance. You can even override the design settings on individual instances.

You can [learn more about Global Templates here](design-system.md#global-templates).

### Mobile First Design

Elements takes a mobile-first design approach. Mobile has now surpassed desktop in global internet usage. Google has switched to mobile-first indexing. That’s why Elements takes a mobile-first approach to website design to ensure your sites work better and rank higher in search results.

While it may feel more natural to some designers to start from a larger, desktop layout and scale downward, CSS doesn’t support a true “desktop-first” cascade. There’s no native way to define base styles at the largest breakpoint and then override them on smaller screens without introducing redundancy or conflicts in your code.

Mobile-first design ensures your site is accessible, performant, and adaptable on all devices, starting from the smallest screen up. Once you get comfortable with this approach, it often leads to cleaner, more maintainable layouts.

We recommend designing at the mobile breakpoint first, and working your way up through the breakpoints to support larger screens.

### Built on Tailwind and AlpineJS

Elements is built upon the popular [Tailwind CSS framework](https://tailwindcss.com/), along with [AlpineJS](https://alpinejs.dev), which makes it a piece of cake to build modern responsive websites. By standardising on the framework used inside Elements, we ensure third-party components work great with every website you build.

### Real-time CSS Generation

Elements builds a custom version of Tailwind CSS in real-time.&#x20;

As you add, remove, or modify any components and content in your project, Elements generates the required CSS, and **only the required CSS**. Elements **does not** load Tailwind from a CDN. Doing so would have severely limited what we are able to do from a design and theming perspective.

To reiterate, **all CSS generation happens in real-time** as you edit your project. It’s truly amazing once you start working with it.

This setup ensures that Elements produces the **smallest amount of CSS possible**, as it only generates the CSS you are _actually using_ in your project.

The way Elements generates CSS for you means there is no need for each developer to write and ship the same CSS over and over again. Elements offers you a modern, reliable, flexible design system that both developers and end users can utilize.

The design system in Elements allows the app, third-party developers, and end users to all create code, components, and content separately but still maintain consistency from a design/theming perspective.

### Learn More About Tailwind

* [Tailwind CSS](https://tailwindcss.com)
* [Tailwind CSS: Utility-First Fundamentals](https://tailwindcss.com/docs/utility-first)
* [Tailwind UI](https://tailwindui.com)
* [Why Tailwind is the Future of CSS Frameworks: A Comparison with Bootstrap](https://b-benjithomas.medium.com/why-tailwind-is-the-future-of-css-frameworks-a-comparison-with-bootstrap-aabe9a9c2166)
* [Why Is TailWind CSS So Great?](https://medium.com/codex/why-is-tailwind-css-so-great-20c407108ae1)\
