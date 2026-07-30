---
description: Build a self-hosted audio player with a styled playlist
---

# Audio

The Audio component creates a self-hosted audio playlist with artwork, track information, progress controls, navigation, and optional visitor volume controls. Add tracks through a collection and style the player to match your site.

### Supported Content and File Types

Each track accepts an audio resource, optional artwork, a title, and an artist. Use browser-compatible audio files and optimised artwork.

### How to Use Audio

You’ll find Audio under **Media** in the Components list.

1. Drag **Audio** onto the page.
2. Add items to the **Tracks** collection.
3. For each track, choose its Audio Source and optionally add Title, Artist, and Artwork.
4. Configure the Now Playing area and track list.
5. Choose which playback and volume controls visitors can use.
6. Preview the complete playlist in a browser.

### Component Settings

#### Tracks

The **Tracks** collection adds, removes, and reorders playlist entries. Each item contains:

* **Title** and **Artist** — Optional text shown in the player.
* **Artwork** — Optional image resource.
* **Audio Source** — The audio resource played for that item.

#### Now Playing

**Layout** is Vertical by default and can be changed to Horizontal. **Gap** defaults to theme spacing 5 and **Padding** to 5 on every side.

**Artwork** controls Size, Shadow, and Radius. Size defaults to theme spacing 48, Shadow to None, and Radius to the theme default.

**Title** and **Artist** each have Color and Size controls. Both colours default to Text 600; Title uses Large and Artist uses Small.

#### Progress Bar

**Background** defaults to Surface 100, **Foreground** to Surface 300, and **Size** to theme spacing 1.5.

#### Track List

**Max Height** defaults to theme spacing 72. Padding defaults to 0 and Gap to 2.

Set the track item Radius, artwork Size, Shadow and Radius, divider Color and Thickness, and Title and Artist text sizes.

Use **State** to style Normal and Hover track colours independently. Each state provides Background, background Opacity, Title colour, and Artist colour. Background opacity defaults to 100%.

#### Icons

**Spacing** between the main controls defaults to theme spacing 6.

**Play and Pause** provides normal Color, Hover colour, Size, and custom Play and Pause SVG resources.

**Next and Previous** is enabled by default. When enabled, set normal and hover colours, size, and custom Next and Previous SVGs.

**Skip Back and Forward** is off by default. Enabling it reveals the same colour, size, and SVG controls.

#### Volume

**Initial Volume** defaults to 100%.

**Visitor Controls** are off by default. When enabled, configure the volume bar Background, Foreground, Size, and Width, plus the mute button’s normal and hover colours, size, and Volume and Muted SVGs.

### Accessibility

Provide meaningful track titles and artist names. Keep playback controls visible and high contrast, and do not start audio automatically.

### Tips and Best Practices

* **Optimise audio files:** Large files increase page load and bandwidth use.
* **Use consistent artwork:** Matching dimensions keep the player stable between tracks.
* **Offer volume control:** Enable visitor controls when audio level may vary between files.

### Related Components

* [Video](video.md) — Plays YouTube, Vimeo, and MP4 video.
* [Image](image.md) — Provides guidance on optimising artwork and alternative text.

{% include "../../.gitbook/includes/common-controls.md" %}
