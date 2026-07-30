---
description: Control generated files and local preview behaviour for your project
icon: screwdriver-wrench
---

# Advanced Settings

The Advanced section lets you fine-tune your project’s output and local preview behaviour. These options are optional but useful when you need more control.

<figure><img src="../../.gitbook/assets/CleanShot 2025-06-01 at 7 .10.29@2x.png" alt="Advanced Project Settings showing site output and local web server options"><figcaption><p>Advanced Section in the Project Settings Window</p></figcaption></figure>

### Site Options

*   **Generate Search Engine Sitemap**

    Automatically creates a sitemap.xml file to help search engines index your site.
*   **Consolidate CSS Files**

    Combines your project’s CSS into fewer files to help reduce page load time.
*   Generate Cache-Busting Links

    Appends unique version strings to assets (like CSS and JS) to ensure browsers always load the latest version.
*   **Minify CSS and JavaScript**

    Strips unnecessary whitespace and comments to shrink file sizes and improve performance.
*   **Anonymize Requests to Third-Party Servers**

    Helps protect your privacy by removing identifiable info from external requests (like Google Fonts or embedded media).

### Default Extension

Sets the file extension used for new pages, typically html, but you can change this to php or others if needed.

### Web Server Port

Configure the local web server used by Elements when previewing your site:

* Auto: Automatically chooses an available port.
* Restart Web Server: Use this if the preview server isn’t running correctly.
* Automatically start web server on document open: Handy if you want preview to be ready as soon as you open a project.
