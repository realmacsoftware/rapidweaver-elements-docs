---
description: Modify the properties of the selected component
icon: sidebar-flip
---

# Inspector

The Component Inspector in Elements lets you edit the properties of the currently selected component. When you click on a component in your design, its available settings appear in the Inspector, giving you full control over how it looks and behaves.

The Inspector is context-aware, meaning the options change depending on which component you have selected. This keeps the interface clean and ensures you only see the settings that are relevant.

{% embed url="https://youtu.be/e3SSIyd9H8U" %}

## Component display modes

Use the display menu beneath the component name in the Inspector to control whether a component appears on the editor canvas and whether it is included in browser previews and published output.

| Option | Editor canvas | Browser preview and published output |
| --- | --- | --- |
| **Visible** | Visible | Included |
| **Hide in Editor** | Hidden | Included |
| **Do Not Publish** | Visible | Excluded |
| **Hide and Do Not Publish** | Hidden | Excluded |

**Hide and Do Not Publish** is useful for unfinished or temporarily disabled content that you want to keep in your project. The component and its content remain in the project, but they do not appear on the editor canvas, in browser previews, or on the published website.

You can still find, select, edit, and restore a hidden component in **Page Layout**.

When you apply **Do Not Publish** or **Hide and Do Not Publish** to a container, the container and everything inside it are excluded from browser previews and published output. The individual display modes stored on its child components are not changed.

### Group Defaults

When you change any value within a group, the group title highlights using the system accent colour. This makes it easy to spot which settings have been modified on a component at a glance.

<figure><img src="../.gitbook/assets/CleanShot 2025-12-17 at 1 .38.00@2x.png" alt="Image component selected with modified Inspector groups highlighted"><figcaption></figcaption></figure>

You can reset an individual control by right-clicking it and choosing **Reset to Default**.

To reset everything in a group back to its defaults, right-click the group heading and choose **Reset Group to Defaults**.

### Inspector Group Modes

To change the display modes in the Component Inspector, right-click on a heading and choose from the following options:

* **Expand All** - Will expand all settings.
* **Collapse All** - Will collapse all open settings.
* **Single Group Mode** - Switching to the single group mode only allows one setting area to be open at a time.

When in Single Group mode the only option available in the right-click menu is switch back to default mode:

* **Single Group Mode** (ticked) — Untick this option to return to the default mode and view multiple settings at the same time.
