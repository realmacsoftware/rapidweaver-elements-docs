---
description: Control generated files and local preview behaviour for your project
icon: screwdriver-wrench
---

# Advanced Settings

The Advanced section lets you fine-tune your project’s output and local preview behaviour. These options are optional but useful when you need more control.

<figure><img src="https://3876014504-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FNy6AECEVH2p4eFDicpM1%2Fuploads%2FTVtOFwLFMgsiQ40GLyCr%2FCleanShot%202025-06-01%20at%207%E2%80%AF.10.29%402x.png?alt=media&#x26;token=a64b954c-3bf5-4b44-9f99-054a4518820b" alt="Advanced Project Settings showing site output and local web server options"><figcaption><p>Advanced Section in the Project Settings Window</p></figcaption></figure>

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
*   **Generate AI Markdown for every page**

    On publish/export, writes a Markdown twin beside each page for AI agents (`index.html.md`, `about.html.md`, and so on). New projects default this on; existing projects stay off until you enable it. Preview does not write these files. Turning the option off does not remove previously uploaded `.md` files from the server. Add a root `llms.txt` (Page Manager → New File, or ask the Assistant) to describe and link your site.

### Default Extension

Sets the file extension used for new pages, typically html, but you can change this to php or others if needed.

### Web Server Port

Configure the local web server used by Elements when previewing your site:

* Auto: Automatically chooses an available port.
* Restart Web Server: Use this if the preview server isn’t running correctly.
* Automatically start web server on document open: Handy if you want preview to be ready as soon as you open a project.
