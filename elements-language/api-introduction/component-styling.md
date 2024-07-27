# Component Styling

### A Standardized Approach

Elements is based on Tailwind, so obviously we use Tailwind for all our components, and highly recommend everyone using and building for Elements does the same.

If everyone is using Tailwind we can **ensure consistency across all components**, making it easier for end users to build sites that are consistent and easy to update.

It also makes collaboration smoother, as everyone follows the same styling method.

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
