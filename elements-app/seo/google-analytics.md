---
description: Adding Google Analytics or Tag Manager Code
---

# Google Analytics

If you’d like to track traffic or integrate services like Google Analytics or Google Tag Manager, you’ll need to add their code snippets to your project. Where you add the code depends on whether you want it to apply to all pages or just one.

### For all pages (site-wide tracking)

To include your tracking code on every page of your site:

1. Open the Site Settings window.
2. Select the Template section.
3. Paste your code into either:
   * Between the `<head>` tags for anything that belongs in the \<head>, such as Google Analytics.
   * Between the after the opening `<body>` tag for things like Google Tag Manager’s \<noscript> block.

This ensures your tracking code is included automatically across every page.

<figure><img src="../../.gitbook/assets/CleanShot 2025-07-02 at 12 .33.37@2x (1).png" alt=""><figcaption><p>Adding site wide code into the Templates area.</p></figcaption></figure>

### For individual pages

If you only want to add tracking code to a specific page:

1. Select the page in the sidebar.
2. Click the Edit Extra Code button in the page Inspector
3. Choose the correct code area from the list on the left (e.g. Head Start, Body Start).
4. Paste your code snippet in the appropriate section.

The code will only be included on that specific page when you publish or preview your site.

<figure><img src="../../.gitbook/assets/CleanShot 2025-07-02 at 12 .40.12@2x.png" alt=""><figcaption><p>Adding code into a specific page.</p></figcaption></figure>
