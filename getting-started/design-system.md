---
description: Learn how the Elements design system works
icon: atom-simple
---

# Core Concepts

Before diving into building your first site, it helps to understand the core concepts that make up Elements. These ideas form the foundation of how the app works and give you a shared language when reading this manual.

You’ll learn about Projects, [Templates](../elements/templates.md), [Themes](../elements/theme-studio/theme.md), [Components](../elements/components/), and [Globals](design-system.md#globals), what each one does, how they fit together, and why they matter. Once you’re familiar with these terms, you’ll be able to navigate Elements more confidently and build sites that are consistent, flexible, and easy to maintain.

### Terminology

Elements uses a consistent design system to keep everything predictable and easy to work with. Whether you’re building a single landing page or a large multi-page site, the same set of terms and tools apply throughout the app.

This section introduces the key concepts you’ll come across: Projects, Templates, Themes, Components, and Globals. Each plays a specific role in how your site is structured, styled, and maintained. Once you understand the difference, you’ll be able to work faster and keep your designs consistent.

#### Projects

A Project is your entire website bundled into one file. It can include multiple pages and all the assets needed for a site. Projects are a great way to kick-start a new build, as they provide a complete setup rather than just a single page layout.

#### Themes

Themes control the overall look and feel of your site. Fonts, colours and general styling are all defined here. Switching themes can instantly give your site a new appearance while leaving the content unchanged.

#### Components

The core Components inside elements represent the basic building blocks of a webpage; they are at the foundation of your page design. They include things like containers, grids, headings, text, and buttons. They are singular items, like Lego bricks.

Some of the more advanced components go beyond the basics; these include things like menus and galleries.

#### Templates

[Templates](../elements/templates.md) are groups of components arranged to create a design or layout. Once you add a template to a page, you can customise it without affecting the original.

The core pack inside of Elements includes a selection of useful layouts for everyday web design, including menus, hero banners, layouts, forms, and more.

You can learn more about [Templates and how they differ to Global Templates here](../elements/templates.md).

#### Globals

[Global Templates](../elements/global-templates.md) (or Globals as they are often called) are user created groups of components. Globals can help maintain a consistent design language across your entire site.

You can reuse global blocks across your site, update the content in one place and have it automatically mirrored to every other instance. This is particularly useful for header and footer sections.

You can take Globals even further by overriding content and design aspects on an individual instance. For example, you might have a banner that you want to use on every page of your site, and you'd like the design to be consistent. You can use the override feature to customise the text and background image on each instance. You can even override the design settings on individual instances.

You can [learn more about Global Templates here](../elements/global-templates.md).

#### In short:

* Use **Projects** when you want a full website starter.
* Use **Themes** when you want to change the overall design style.
* Use **Components** as the reusable building blocks of your pages.
* Use **Templates** when you want a pre-built sections.
* Use **Globals** to control site-wide, linked components or layouts (perfect for Navigation and Footer)

### Design System

Elements takes a mobile-first design approach. Mobile has now surpassed desktop in global internet usage. Google has switched to mobile-first indexing. That’s why Elements takes a mobile-first approach to website design to ensure your sites work better and rank higher in search results.

While it may feel more natural to some designers to start from a larger, desktop layout and scale downward, CSS doesn’t support a true “desktop-first” cascade. There’s no native way to define base styles at the largest breakpoint and then override them on smaller screens without introducing redundancy or conflicts in your code.

Mobile-first design ensures your site is accessible, performant, and adaptable on all devices, starting from the smallest screen up. Once you get comfortable with this approach, it often leads to cleaner, more maintainable layouts.

We recommend designing at the mobile breakpoint first, and working your way up through the breakpoints to support larger screens.

### Built on Tailwind and AlpineJS

Elements uses the popular [Tailwind CSS framework](https://tailwindcss.com/) alongside [Alpine.js](https://alpinejs.dev), making it easier to build modern, responsive websites. Standardising on the frameworks used by Elements helps third-party components work consistently across your projects.

### Real-time CSS Generation

Elements builds a custom version of Tailwind CSS in real time.

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
* [Why Is TailWind CSS So Great?](https://medium.com/codex/why-is-tailwind-css-so-great-20c407108ae1)<br>
