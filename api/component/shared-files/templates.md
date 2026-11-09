---
description: Shared Template Folder
---

# Templates

The `templates` folder contains HTML or PHP files that are injected into the page when any component from your pack is used. These templates typically load [shared assets](assets.md) or add global scripts and styles.

## Injection Points

Templates must be placed in one of four subfolders, each corresponding to a specific location in the HTML document:

| Folder | Location | Use Cases |
|--------|----------|-----------|
| `headStart` | Start of `<head>` | Core libraries that must load first, polyfills |
| `headEnd` | End of `<head>` | Styles, deferred scripts, additional libraries |
| `bodyStart` | Start of `<body>` | Early initialization, loading indicators |
| `bodyEnd` | End of `<body>` | Feature scripts, animations, scroll handlers |

## Folder Structure

```
shared/
  templates/
    headStart/
      setup.html
    headEnd/
      styles.html
      directives.html
    bodyEnd/
      animations.html
```

You can have multiple template files in each folder. There is no restriction on file naming—all files in each folder will be included.

## Supported File Types

| Type | Description |
|------|-------------|
| `.html` | HTML content, inline scripts, inline styles |
| `.php` | PHP code for server-side processing |

Templates can contain inline code within `<script>` and `<style>` tags, as well as references to shared assets using `{{assetPath}}`.

## Single Inclusion

Shared templates are included **once per page** per element pack, regardless of how many components from that pack are on the page. This ensures libraries and initialization code are not duplicated.

{% hint style="info" %}
HTML, PHP, CSS, and JS files are supported in the [Templates folder at the single Component](../templates/) level for component-specific templates.
{% endhint %}
