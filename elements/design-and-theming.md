---
description: Build a consistent responsive design system with themes, breakpoints and dark mode
icon: palette
---

# Design and Theming

Elements uses a project-wide design system to keep colours, typography, spacing, borders, shadows, and responsive behaviour consistent.

### Theme Studio

[Theme Studio](theme-studio/README.md) is where you choose a theme and configure the shared values used by components throughout the project.

Its sections cover:

* Theme selection and creation.
* Responsive screens and container widths.
* Page colours.
* Colour palettes.
* Font families and sizes.
* Spacing, shadows, border widths, and border radii.
* Typography rules for paragraphs, headings, code, quotations, lists, and links.

### Breakpoints

[Breakpoints](responsive-breakpoints.md) control where responsive property overrides begin. Elements follows a mobile-first system, so a value continues into larger breakpoints until it is overridden.

### Dark Mode

[Dark Mode](dark-mode.md) lets the design respond to the visitor’s system or browser appearance. Theme colours provide paired light and dark values so components can switch consistently.

### Recommended Workflow

1. Choose or create a Theme.
2. Set the responsive Screens and container widths.
3. Define the primary colour roles and dark-mode values.
4. Choose fonts, type sizes, and Typography rules.
5. Establish spacing, borders, radii, and shadows.
6. Build pages with theme values before adding local overrides.
