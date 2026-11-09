# rw.component

The `rw.component` object provides metadata about the component itself, including paths to assets.

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `title` | String | The component's name |
| `group` | String | The component group/category |
| `version` | Integer | Component version number (not the Elements app — see [`rw.system`](rw.system.md)) |
| `build` | Integer | Component build number (not the Elements app — see [`rw.system`](rw.system.md)) |
| `assetPath` | String | Path to component-specific assets |
| `siteAssetPath` | String | Path to site-level component assets |
| `sharedAssetPath` | String | Path to shared pack assets |

## Accessing Component Data

```javascript
const transformHook = (rw) => {
    const {
        title,
        assetPath,
        sharedAssetPath
    } = rw.component;

    console.log(title);           // "Image Gallery"
    console.log(assetPath);       // "/resources/components/gallery/"
    console.log(sharedAssetPath); // "/resources/shared/"
};

exports.transformHook = transformHook;
```

## Using Asset Paths

Asset paths are essential for referencing component resources like images, scripts, and stylesheets:

```javascript
const transformHook = (rw) => {
    const { assetPath, sharedAssetPath } = rw.component;

    rw.setProps({
        // Component-specific assets
        placeholderImage: `${assetPath}/images/placeholder.png`,
        componentScript: `${assetPath}/js/gallery.js`,

        // Shared assets across the pack
        sharedIcon: `${sharedAssetPath}/icons/arrow.svg`,
        sharedStyles: `${sharedAssetPath}/css/common.css`
    });
};

exports.transformHook = transformHook;
```

## Placeholder Images in Edit Mode

A common pattern is showing placeholder images while editing:

```javascript
const transformHook = (rw) => {
    const { mode } = rw.project;
    const { sharedAssetPath } = rw.component;
    const { image } = rw.props;

    const isEditMode = mode === 'edit';
    const hasImage = image && image.image;

    // Show placeholder in edit mode when no image is set
    const displayImage = hasImage
        ? image.image
        : (isEditMode ? `${sharedAssetPath}/images/placeholder.png` : null);

    rw.setProps({
        displayImage,
        hasImage
    });
};

exports.transformHook = transformHook;
```

## Using in Templates

```html
<!-- Component-specific assets -->
<img src="{{assetPath}}/images/icon.png" alt="Icon">

<!-- Shared pack assets -->
<link rel="stylesheet" href="{{sharedAssetPath}}/css/styles.css">

<!-- Conditionally load scripts -->
@if(needsGalleryScript)
    <script src="{{assetPath}}/js/gallery.min.js"></script>
@endif
```
