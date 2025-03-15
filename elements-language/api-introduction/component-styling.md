---
description: A standardised approach
---

# Component Styling

Elements is based on Tailwind. We use Tailwind for all our components, and highly recommend everyone using and building for Elements does the same.

If everyone is using Tailwind (and the built-in Theme UI Controls) we can **ensure consistency across all components**, making it easier for end users to build sites that are consistent and easy to update.

It also makes collaboration smoother, as everyone follows the same styling method.

**Your main goal should always be to make a component that feels native to Elements.**

### Consistency for the User

In Elements, all styling configurations—such as colors, fonts, and sizes—are controlled by the Theme (which anyone can create) and managed through the Theme Studio (where users can customize the styling to their needs).

Components shouldn't dictate custom styling; instead, they inherit styles from the Tailwind themes. **The theme informs the components how they should look, ensuring consistency across all components, whether they are built-in, third-party, or custom-made.** This approach ensures that users can switch themes seamlessly without breaking their site’s design.

Allowing components to dictate their own styles will lead to inconsistencies, making it unclear whether a component will “just work” within a given project. That’s why components rely on the values defined in the Theme Studio as their defaults, ensuring uniformity. They are not opinionated about the actual values—they just need to know that a value exists for each style.

For example, let’s say you have a Heading component. You want to set a default font family and font size. In your properties.json, you would define the default font family as heading and the default font size as 3xl.

The component doesn’t concern itself with the specific values of these properties; it only cares that they exist. This allows themes and users to fully customize the styles while ensuring that all components “just work” in any project.

### Important: Use Theme Controls

When designing your Component, you should always use the Theme-based UI Controls wherever possible; these include the following:

* [Theme Border Width](../bundle-structure/components/properties.json/ui-controls/theme-border-width.md)
* [Theme Border Radius](../bundle-structure/components/properties.json/ui-controls/theme-border-radius.md)
* [Theme Color](../bundle-structure/components/properties.json/ui-controls/theme-color.md)
* [Theme Font](../bundle-structure/components/properties.json/ui-controls/theme-font.md)
* [Theme Spacing](../bundle-structure/components/properties.json/ui-controls/theme-spacing.md)
* [Theme Shadow](../bundle-structure/components/properties.json/ui-controls/theme-shadow.md)
* [Theme Text Style](../bundle-structure/components/properties.json/ui-controls/theme-text-style.md)
* [Theme Typography](../bundle-structure/components/properties.json/ui-controls/theme-typography.md)

### Default Colours

Tailwind (and Elements) includes an expertly-crafted default color palette out-of-the-box - you should take advantage of that and use it.

All components **need to work out of the box**.  A good guide is to use "Brand" for things like buttons, and "Text" for the text colours, and "Surface" for background colours.

### Utility-First Approach

Tailwind offers a utility-first approach to styling. This means you apply small, reusable utility classes directly to your HTML elements. Instead of writing a lot of custom CSS, you can compose styles using these predefined classes.

### Direct Application in Templates

Instead of writing custom CSS you should use Tailwind utilities directly in your template. This means adding classes like `bg-blue-500`, `text-center`, or `mt-4` right on your HTML elements. This way, you remove the need for scoped CSS because each component’s styles are already self-contained.

### Preventing Style Leakage

Because Tailwind styles are applied directly to DOM elements using utility classes we prevent style leakage between components. Each component’s styles stay within its HTML structure meaning they don’t affect other components or pages on your site.

### Customization with Properties

For customization, you can use properties to generate Tailwind classes ready to use within your templates. This way, you keep flexibility while sticking to the utility-first approach.

### Optimized CSS Generation

In summary, the custom CSS in your component templates should use Tailwind classes. This change removes the need for scoped CSS and keeps all styling within Tailwind. Elements can then generate only the CSS your page uses, since it builds Tailwind locally and includes just the necessary utilities. This results in a smaller, more efficient CSS file(s).

***

### I really NEED to scope my CSS

If you’ve read all too the above and are still saying to yourself “great…but I really need to use custom/scoped CSS!” then there is a way but only use this as a last resort!

You can manually “scope” your CSS classes by using the component’s ID in your Template and Styles. Ahiwl this is not strictly “scoped CSS”, it will encapsulate the CSS to each individual component instance.

In your styles you can do something like:

```bash
.{{id}} {
    ...
}

.{{id}} .child-element {
    ...
}
```

And in your Template file:

```perl
<div class="{{id}} ...">...</div>
```

Remember; If you add custom CSS it will not be controllable from the Theme Studio, thus resulting in a worse user experiance.
