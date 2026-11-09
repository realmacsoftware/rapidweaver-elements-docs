---
icon: folder-closed
---

# Shared Files

The `shared` folder lives inside the `components/` directory and provides a central location for assets and templates that are used by multiple components in your element pack. This eliminates duplication when several components need access to the same JavaScript libraries, stylesheets, or other resources.

## When to Use Shared Files

Use shared files when:

- Multiple components in your pack depend on the same JavaScript library (e.g., Alpine.js, GSAP)
- You need global CSS fixes or styles that apply across components
- Components share common images, fonts, or other media assets
- You want to inject initialization scripts or configuration once per page

## Folder Structure

```
MyElementPack.elementsdevpack/
  components/
    shared/
      assets/                 # Shared assets (JS, CSS, images, fonts, etc.)
        images/               # Subdirectories supported for organization
      templates/              # HTML/PHP templates injected into pages
        headStart/            # Injected at start of <head>
        headEnd/              # Injected at end of <head>
        bodyStart/            # Injected at start of <body>
        bodyEnd/              # Injected at end of <body>
```

## Single Inclusion Behavior

Shared files are only included **once per page**, regardless of how many components from your pack are added. This ensures libraries and styles are not duplicated and allows you to safely include dependencies that multiple components rely on.

## Learn More

- [Assets](assets.md) - Store JavaScript, CSS, images, fonts, and other files
- [Templates](templates.md) - Inject HTML or PHP at specific locations in the page
