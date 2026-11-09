# Assets

The `assets` folder stores files that are shared across multiple components in your element pack. Assets are **not automatically included** in the page—they must be referenced from a [shared template](templates.md).

## Supported Asset Types

| Type | Examples |
|------|----------|
| JavaScript | Libraries (Alpine.js, GSAP), utility scripts, plugins |
| CSS | Stylesheets, resets, utility classes |
| Images | Icons, placeholders, UI graphics |
| Fonts | Custom web fonts |
| Other | Any static file your components need |

## Folder Organization

You can organize assets into subdirectories for better structure:

```
shared/
  assets/
    alpine.js
    gsap.min.js
    styles.css
    images/
      icon.webp
      placeholder.jpg
    fonts/
      custom-font.woff2
```

## Linking to Assets

Use the `{{assetPath}}` variable in your shared templates to reference assets. This resolves to the correct path at build time.

**JavaScript:**
```html
<script src="{{assetPath}}/library.js"></script>
```

**CSS:**
```html
<link rel="stylesheet" href="{{assetPath}}/styles.css">
```

**Images:**
```html
<img src="{{assetPath}}/images/icon.png">
```

{% hint style="info" %}
Assets are only accessible when referenced from a shared template. Place the template in the appropriate injection folder (`headStart`, `headEnd`, `bodyStart`, or `bodyEnd`) based on when the asset should load.
{% endhint %}
