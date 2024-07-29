# Migrating your stacks

{% hint style="info" %}
This document is not finished… It will provide examples on how to convert a stack into a native Element Component.
{% endhint %}

This document only applies to existing developers that build stacks for RapidWeaver Classic. If you are a new developer to the Elements platform you can safely ignore this document.

To convert classic stacks to an Element Component it will unfortunately need to be re-written. However, once you get familiar with how the properties JSON file is constructed, you'll find converting your stack info.plist into this new format is fairly straightforward (and much more enjoyable to work with).

Porting your stack(s) over to Elements will also give you the chance to bring it up-to-date, making sure it's fully WYSIWYG, and uses the built-in Tailwind CSS theming system.

You can learn more about why your converted Stack must use Tailwind CSS in the [Component Styling](component-styling.md) section of this manual. We also recommended reading the [Design System](../../user-guide/design-system.md) section of this manual.
