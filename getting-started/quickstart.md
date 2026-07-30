---
description: Step-by-step guide to building your first website in Elements
icon: bolt
---

# Quickstart

Follow our step-by-step guide to building your first website in Elements.

{% hint style="info" %}
New to the terminology? Read [Core Concepts](design-system.md) alongside this guide. When you are ready for a more detailed walkthrough, continue with [Let's Build](quickstart/lets-build.md).
{% endhint %}

### 5-Minute Quick Start Guide

If you’re new to Elements, this five-minute video shows you how to build a page using Templates and explore a ready-made project.

{% embed url="https://youtu.be/19f5r940LbI" %}

### Building Your First Website: A Brief Outline

_This_ [_walkthrough was written by Tom Hogan_](https://forums.realmacsoftware.com/t/guidelines/55711/2?u=dan) _on the Elements Forum — Thanks Tom_ 👋

In a new blank project:

1. Choose your fonts (family and sizes).
2. Establish your brand colours and add other colour choices if necessary.
3. Choose your breakpoint sizes.

These are all design choices, but defining them in the theme early will prevent inconsistencies later. Explore other websites and the free Elements projects for ideas.

4. On your home page, create a Menu, Container and Footer. Refine the menu and footer, then convert them to Globals. If every page will use the same Flex or Grid structure inside the Container, add that too.
5. Establish your basic page structure (you can add to it later) with blank pages that are named (home, blog, gallery, contact, etc.). You can add sub-pages later. Add the Header/Container/Footer construct to each page.
6. Add the SVG, JPG, PNG and other assets you expect to use. Organise Resources with a folder structure that reflects your pages, such as `/resources/images/page/resource.xxx`.
7. If you plan to use Elements CMS, add the required folders and files, then add Posts and Authors pages to the structure created in step 5.
8. Design with the built-in components and any add-ons you need. A mobile-first workflow is often easiest: begin at the smallest screen, then add breakpoint overrides as the available space increases.
9. Add your final page and CMS content. Placeholder text can help you concentrate on the design before the copy is ready.
10. Preview the entire site and check every page.

Use lowercase names for files, folders, pages and resources. Avoid spaces; use hyphens between words instead.

### An Introduction to the Elements Interface

While the following video does not cover every feature, it provides a high-level overview of the app’s layout and workflow. You’ll see how to add components, navigate the editor and begin building a website.

Use this as a quick tour of the basics before exploring the rest of the manual.

{% embed url="https://youtu.be/zas7L3rMX18" %}

### Ready-Made Projects to Explore and Use

Elements includes a selection of free, ready-made projects. Use them to launch a site quickly or learn by exploring how their pages were built.

<figure><img src="../.gitbook/assets/CleanShot 2025-09-17 at 2 .50.18@2x.png" alt="Elements project chooser displaying a collection of ready-made starter projects"><figcaption></figcaption></figure>

### Optimise Media before Importing

Prepare and **optimise media for the web** before importing it, particularly video, audio and high-resolution images. Uncompressed or oversized files can increase the project size and slow down both Elements and the published website.

We recommend:

* **Compressing images** with tools such as Squash, TinyPNG or ImageOptim.
* **Optimising videos** as MP4 (H.264), reducing their resolution or bitrate where appropriate.
* **Hosting large files externally**, including video, audio and PDFs, then linking to their URLs. This keeps the project smaller and easier to manage.

{% include "../.gitbook/includes/elements-website-hosting.md" %}
