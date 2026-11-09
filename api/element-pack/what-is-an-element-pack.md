---
description: Learn more about the Element Pack format
icon: circle-question
---

# What is an Element Pack?

An Element Pack is a folder-based “plugin” format for sharing and distributing addons for Elements.

* Development Use Only: An Element Pack ends with a `.elementsdevpack` extension. This format is strictly for development environments and should not be sold or shared in this form.
* Distributable Version (Coming soon): To share your packs with others you'll use the Elements Store. Distributable packs are non-editable, pre-processed, optimised and encrypted to protect your code. You can [learn more about distributing your addons here](../../store/partners/pack-distribution.md).

### What Can You Include?

Your Element Pack can bundle together different types of add-ons, such as any combination of the following:

* [Components](../component/components.md) – Reusable, structured elements
* [Resources](../resource/what-are-resources.md) – Assets like images or other files
* [Templates](../template/what-are-templates.md) – Pre-built sections consisting of multiple components
* [Themes](../theme/what-are-themes.md) – Predefined visual styles
* [Projects](../project/what-are-projects.md) – (Planned for future support)

Note: Element Packs must follow the macOS “bundle” structure. Templates, Resources, and Themes are created within Elements whereas Components are typically built outside of Elements using an editor like VS Code.

### Folder Structure Overview

Here’s how a typical `.elementsdevpack` bundle is organized:

```
MyElementPack.elementsdevpack/
├── info.json
├── components/
│   ├── com.companyname.slideshow/
│   ├── com.companyname.navbar/
│   └── shared/
│       ├── assets/
│       └── templates/
└── themes/
    ├── com.companyname.themes.architect/
    └── com.companyname.themes.solar/
```

#### Folder Breakdown:

* Root folder (MyElementPack.elementsdevpack)
  * [info.json](info.json.md) - \[required] the main configuration file for the pack
  * components - contains folders for each custom component
  * themes - contains folders for each custom theme

### Tips for Getting Started

* Start with info.json: This is your pack’s “manifest.” Set it up properly before adding components.
* Add one thing at a time:
  * _Components_ need extra structure, create them carefully.
  * _Themes_, _templates_, and _resources_ are more straightforward and should be added using the Elements app.
* Include Shared Files: If multiple components rely on the same assets (for example, icons or CSS), put them in the components/shared/ folder for easy access and organization.
* Before Distributing (Coming soon): Convert Dev Packs to a secure format via the Elements Store, which encrypts your code and makes it safe to share.&#x20;
