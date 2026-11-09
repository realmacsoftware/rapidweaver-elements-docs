---
description: Streamline your workflow with Component Build Tools
---

# Build Tools

Build powerful, reusable web components for RapidWeaver without the complexity. This toolkit handles the heavy lifting so you can focus creating awesome components.

{% embed url="https://youtu.be/X_57memVXHk" %}

{% hint style="warning" %}
For more detailed information about this package, including installation details and examples, please visit the [rw-elements-tools readme.md](https://www.npmjs.com/package/rw-elements-tools)
{% endhint %}

## RW Elements Tools

**Official NPM Toolkit for RapidWeaver Elements Development**

[rw-elements-tools](https://www.npmjs.com/package/rw-elements-tools) is the official utility package for developers working with **RapidWeaver Elements**. It provides a set of helpful tools and build helpers that make creating, compiling, and maintaining Elements packs simpler and more efficient.

Whether you’re just getting started with Elements development or building advanced component packs, RW Elements Tools helps streamline your workflow so you can focus on building great experiences.

***

### What is RW Elements Tools?

RW Elements Tools is a developer toolkit published on NPM that supports the Elements development workflow.

It includes utilities designed to help with:

* Building and bundling Elements components
* Running common development and build tasks
* Standardising workflows across Elements projects
* Preparing packs for production use

The tools are designed to work out of the box with minimal setup and sensible defaults.

**View the package on NPM**\
[https://www.npmjs.com/package/rw-elements-tools](https://www.npmjs.com/package/rw-elements-tools)

***

### Why it exists

Building Elements packs often involves repetitive setup and tooling work. RW Elements Tools exists to remove friction and provide a shared, reliable foundation for Elements development.

Using this toolkit helps:

* Reduce boilerplate configuration
* Keep projects consistent across teams
* Improve build reliability
* Speed up development and iteration

It’s the same tooling used and maintained alongside the Elements ecosystem.

***

### Who is it for?

RW Elements Tools is ideal for:

* **Developers** building custom Elements packs
* **Teams** working on multiple Elements projects
* **Open source contributors** supporting Elements tooling
* Anyone creating, testing, or publishing Elements components

If you’re writing code for Elements, this package is designed to fit naturally into your workflow.

***

### Installing and using RW Elements Tools

Installation and usage instructions are maintained on the NPM package page.

To learn how to install the toolkit, configure it for your project, and use the available utilities, visit:

👉 [https://www.npmjs.com/package/rw-elements-tools](https://www.npmjs.com/package/rw-elements-tools)

***

### Contributing

RW Elements Tools is open to contributions from the community.

You can help by:

* Reporting bugs or issues
* Suggesting improvements or enhancements
* Submitting pull requests
* Helping improve documentation and examples

Contribution links and repository details can be found via the NPM page.

***

### Links

* **NPM Package**\
  [https://www.npmjs.com/package/rw-elements-tools](https://www.npmjs.com/package/rw-elements-tools)
* **Installation & Usage**\
  See the package page on NPM

***

## Installation

```bash
npm install --save-dev rw-elements-tools
```

## Usage Overview

### Controls in properties.config.json

```json
{
  "globalControl": "Spacing"
}
```

### Properties in controls

```json
{
  "select": {
    "use": "FontWeight"
  }
}
```

### Shared Hooks in hooks.source.js

```javascript
function transformHook(rw) {
    const classes = classnames()
        .add(globalSpacing(rw))
        .add(globalBackground(rw))
        .toString();

    return { classes };
}
```

For installation details and full documentation, visit [NPM](https://www.npmjs.com/package/rw-elements-tools).

***

| Section                       | Description                                         | Count |
| ----------------------------- | --------------------------------------------------- | ----- |
| [Controls](controls/)         | UI control definitions for `properties.config.json` | 90+   |
| [Properties](properties/)     | Reusable value definitions (`use` references)       | 13    |
| [Shared Hooks](shared-hooks/) | JavaScript utility functions for `hooks.source.js`  | 35+   |
