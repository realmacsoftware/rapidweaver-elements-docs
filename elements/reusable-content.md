---
description: Reuse complete layouts with Templates and linked Globals
icon: clone
---

# Templates and Globals

Templates and Globals both help you reuse groups of components, but they solve different problems.

| Feature | Templates | Globals |
| --- | --- | --- |
| Best for | Starting a new layout quickly | Repeating content across several pages |
| Connection after adding | Independent copy | Remains linked |
| Later edits | Affect only that copy | Can update every linked instance |
| Common examples | Hero sections, feature grids, forms | Menus, headers, footers, announcements |

### Templates

[Templates](templates.md) are reusable starting points. After adding one to a page, its components become an independent layout that can be changed without affecting the original Template or other copies.

### Globals

[Globals](global-templates.md) remain linked wherever they are used. Update the Global once to keep shared structures and content consistent throughout the project.

{% hint style="info" %}
Use a Template when each copy should evolve independently. Use a Global when every instance should continue sharing the same source.
{% endhint %}

### Recommended Workflow

1. Build and test the component layout on a page.
2. Decide whether future copies should remain linked.
3. Save independent starting points as Templates.
4. Save site-wide or repeatedly maintained content as Globals.
5. Preview changes on every page where the layout appears.
