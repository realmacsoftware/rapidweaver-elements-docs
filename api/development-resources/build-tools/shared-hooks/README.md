---
description: JavaScript utility functions for hooks.source.js
---

# Shared Hooks

Call these functions in your `hooks.source.js`. No imports needed - they're automatically available.

## Animations

| Function | Description |
|----------|-------------|
| `globalAnimations()` | [Details](animations/global-animations.md) |
| `globalReveal()` | [Details](animations/global-reveal.md) |

## Background

| Function | Description |
|----------|-------------|
| `globalBackground()` | [Details](background/global-background.md) |
| `globalBgColor()` | [Details](background/global-bg-color.md) |
| `globalBgGradient()` | [Details](background/global-bg-gradient.md) |
| `globalBgImage()` | [Details](background/global-bg-image.md) |
| `globalBgImageFetchPriority()` | [Details](background/global-bg-image-fetch-priority.md) |
| `globalBgVideoThumbnail()` | [Details](background/global-bg-video-thumbnail.md) |

## Borders

| Function | Description |
|----------|-------------|
| `globalBorders()` | [Details](borders/global-borders.md) |
| `globalOutline()` | [Details](borders/global-outline.md) |

## Core

| Function | Description |
|----------|-------------|
| `addPrefixToTailwindClasses()` | [Details](core/add-prefix-to-tailwind-classes.md) |
| `advancedClasses()` | [Details](core/advanced-classes.md) |
| `classnames()` | [Details](core/classnames.md) |
| `getHoverPrefix()` | [Details](core/get-hover-prefix.md) |
| `globalHTMLTag()` | [Details](core/global-html-tag.md) |
| `injectPrefixOnDarkModeColors()` | [Details](core/inject-prefix-on-dark-mode-colors.md) |

## Effects

| Function | Description |
|----------|-------------|
| `bgPosition()` | [Details](effects/bg-position.md) |
| `globalEffects()` | [Details](effects/global-effects.md) |
| `globalFilters()` | [Details](effects/global-filters.md) |
| `globalOverlay()` | [Details](effects/global-overlay.md) |
| `globalOverlayColor()` | [Details](effects/global-overlay-color.md) |
| `globalOverlayGradient()` | [Details](effects/global-overlay-gradient.md) |
| `globalOverlayImage()` | [Details](effects/global-overlay-image.md) |

## Interactive

| Function | Description |
|----------|-------------|
| `globalFilter()` | [Details](interactive/global-filter.md) |
| `globalLink()` | [Details](interactive/global-link.md) |

## Layout

| Function | Description |
|----------|-------------|
| `getHiddenClasses()` | [Details](layout/get-hidden-classes.md) |
| `globalActAsGridOrFlexItem()` | [Details](layout/global-act-as-grid-or-flex-item.md) |
| `globalLayout()` | [Details](layout/global-layout.md) |

## Navigation

| Function | Description |
|----------|-------------|
| `globalMenuItem()` | [Details](navigation/global-menu-item.md) |
| `globalNavItems()` | [Details](navigation/global-nav-items.md) |
| `globalNavTitle()` | [Details](navigation/global-nav-title.md) |

## Sizing

| Function | Description |
|----------|-------------|
| `aspectRatioClasses()` | [Details](sizing/aspect-ratio-classes.md) |
| `globalSizing()` | [Details](sizing/global-sizing.md) |
| `globalSizingContainer()` | [Details](sizing/global-sizing-container.md) |
| `objectClasses()` | [Details](sizing/object-classes.md) |

## Spacing

| Function | Description |
|----------|-------------|
| `globalSpacing()` | [Details](spacing/global-spacing.md) |
| `globalSpacingMargin()` | [Details](spacing/global-spacing-margin.md) |
| `globalSpacingPadding()` | [Details](spacing/global-spacing-padding.md) |

## Transforms

| Function | Description |
|----------|-------------|
| `globalTransforms()` | [Details](transforms/global-transforms.md) |

## Transitions

| Function | Description |
|----------|-------------|
| `aControlWantsHover()` | [Details](transitions/a-control-wants-hover.md) |
| `getAlpineTransitionAttributesDesktop()` | [Details](transitions/get-alpine-transition-attributes-desktop.md) |
| `getAlpineTransitionAttributesMobile()` | [Details](transitions/get-alpine-transition-attributes-mobile.md) |
| `globalTransitions()` | [Details](transitions/global-transitions.md) |

## Typography

| Function | Description |
|----------|-------------|
| `globalButtonFontAndTextStyles()` | [Details](typography/global-button-font-and-text-styles.md) |
| `globalHeadingColor()` | [Details](typography/global-heading-color.md) |
| `globalHeadingTextColor()` | [Details](typography/global-heading-text-color.md) |
| `globalInputFontAndTextStyles()` | [Details](typography/global-input-font-and-text-styles.md) |
| `globalTextFontsAndTextStyles()` | [Details](typography/global-text-fonts-and-text-styles.md) |

## Quick Usage

```javascript
function transformHook(rw) {
    const classes = classnames()
        .add(globalSpacing(rw))
        .add(globalBackground(rw))
        .toString();

    return { classes };
}

exports.transformHook = transformHook;
```
