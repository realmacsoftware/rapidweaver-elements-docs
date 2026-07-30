---
description: Manage the look and feel of your website
icon: masks-theater
---

# Theme Studio

Theme Studio is the project-wide design system in Elements. It controls the reusable colours, fonts, text sizes, spacing, shadows, borders, typography, page background, and responsive screens available throughout your website.

When a component uses a Theme Studio value, changing that value updates every instance that references it. This makes Theme Studio the best place to establish a consistent design before adjusting individual components.

{% embed url="https://youtu.be/npoc1vewTSw" %}

### Open Theme Studio

1. Open an Elements project.
2. Choose **Theme Studio** from the project toolbar.
3. Select a section in the sidebar.
4. Adjust a theme value or add a custom value for the current project.
5. Review the result at each enabled breakpoint and in light and dark appearance.

### Theme Studio Sections

* [**Theme**](theme.md) — Choose the design foundation for the project.
* [**Screens**](screens.md) — Configure responsive breakpoints and container widths.
* [**Page**](page.md) — Set the default light and dark page background.
* [**Colors**](colors.md) — Manage colour roles, shade scales, and custom palettes.
* [**Font Family**](font-family.md) — Configure system, resource, and Google fonts.
* [**Font Size**](font-style.md) — Manage the reusable type scale.
* [**Spacing**](spacing.md) — Add reusable spacing values.
* [**Shadows**](shadows.md) — Define reusable shadow treatments.
* [**Border Width**](border-width.md) — Manage the site-wide border scale.
* [**Border Radius**](border-radius.md) — Manage reusable corner-radius values.
* [**Typography**](typography.md) — Style paragraphs, headings, lists, quotes, code, and links as a set.

### Use Theme Defaults

Use the named theme values whenever possible. They keep your site consistent and help built-in Components and Templates adapt when you change theme.

* **Colours:** Use **Brand**, **Accent**, **Surface**, and **Text**. These are managed in the Theme Studio and ensure that components, templates, and layouts all work together seamlessly.
* **Defaults:** For **Border Width**, **Border Radius**, and **Shadows**, start with the built-in **Default** option.
* **Typography:** For text, use the predefined roles: **Heading**, **Body**, **Code**, and **Quote**. These are designed to work harmoniously and adjust automatically when you change your theme.
* **Spacing:** Reuse the theme scale instead of entering a different one-off value for every component.

{% hint style="info" %}
Use custom values when they express a genuine part of the design system. For a one-off exception, a component-level custom value may be more appropriate.
{% endhint %}

### Recommended Workflow

1. Choose a theme.
2. Set Brand, Accent, Surface, and Text colours.
3. Choose the Heading, Body, Code, and Quote font families.
4. Review Font Size, Spacing, Border Radius, Border Width, and Shadows.
5. Configure the Article typography preset.
6. Confirm Page colours and Screens.
7. Build components using those shared values.

This order gives components stable design tokens to work with and makes later site-wide changes much easier.
