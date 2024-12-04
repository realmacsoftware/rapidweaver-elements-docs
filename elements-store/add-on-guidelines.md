---
description: A guide to making sure your add-ons meets user expectations
---

# Add-on Guidelines

To give users a seamless experience when using built-in and third-party components you should ensure all your add-ons meet the requirements list below.

{% hint style="info" %}
This document is a work-in-progress.
{% endhint %}

## Elements Component Checklist

* [ ] Component is fully WYSIWYG in the Editor:
  * [ ] The Editor looks the same as Preview
  * [ ] Settings and Admin options are not visible in the Editor (place these in the Inspector)
* [ ] Component uses Tailwind CSS:
  * [ ] Component styling uses Tailwind classes found in the Theme Studio
  * [ ] Takes advantage of the Theme based [UI controls](../elements-language/properties.json/ui-controls/)!
* [ ] Components should not parse @text or @typography data in their hooks.js files
