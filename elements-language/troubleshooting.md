---
icon: circle-question
---

# Troubleshooting

This document outlines some of the "gotchas" that Users developing Components for Elements have run into.

### Dynamic PHP Code and Tailwind Classes Generation

If you’re using PHP to dynamically generate Tailwind classes, you may run into an issue where the styles don’t apply correctly. This happens because Elements builds Tailwind CSS on the fly.

When you preview or export your site, Tailwind only includes the classes that are present in the code at that moment. If your PHP code generates Tailwind classes _after_ this process (e.g., inserting them dynamically when the page loads), Tailwind won’t recognize those classes, and the corresponding styles won’t be available.

#### Workaround

If you know in advance which Tailwind classes your PHP code will generate, you can write them out into your page to ensure Elements/Tailwind includes them on preview/export. For example:

```html
<!-- Hidden divs to include all possible Tailwind classes -->
<div class="hidden bg-red-500 bg-blue-500 bg-green-500"></div>
```

To learn more about read [Just-in-Time friendly style variants in Tailwind CSS UI components](https://www.protailwind.com/just-in-time-friendly-style-variants-in-tailwind-css-ui-components-part-1), and a way to work around this, [this thread in the Elements Forum](https://forums.realmacsoftware.com/t/php-code-dynamic-tailwind-classes-heads-up/46302).
