---
description: Step-by-step guide to building your first website in Elements.
icon: bolt
---

# Quickstart

Follow our step-by-step guide to building your first website in Elements.

### 5-Minute Quick Start Guide

If you're new to Elements, this 5-minute quick start guide will help you get started building your first page, fast! In the video, we'll show you how to build a page using Templates, and navigate a pre-built marketplace project.

{% embed url="https://youtu.be/19f5r940LbI" %}

### Building Your First Website: A Brief Outline

_This_ [_walkthrough was written by Tom Hogan_](https://forums.realmacsoftware.com/t/guidelines/55711/2?u=dan) _on the Elements Forum — Thanks Tom_ 👋

In a new blank Project:

1. Choose your fonts (family and sizes).
2. Establish your brand colours at a minimum, more colour choices if necessary.
3. Choose your breakpoint sizes.

The above are all style issues, but if they’re not in the Theme, then you’re going to have lots of issues downstream. Look at what other sites do as examples to get ideas for Theme. Looking at the free projects is one way of seeing how they’re set up in the theme.

4. On your home page, create the following Component structure: (a) Menu, (b) Container, (c) Footer. Keep tweaking your menu and footer until you like them, then make them globals. It’s possible that you might want to put Flex/Grid in the Container between them that will be consistent across pages, if so, do that next.
5. Establish your basic page structure (you can add to it later) with blank pages that are named (home, blog, gallery, contact, etc.). You can add sub-pages later. Add the Header/Container/Footer construct to each page.
6. For as many of the SVG, JPG, PNG, and other assets you’re going to use on the site, build out the Resources section with a folder structure that matches the page structure you just created (e.g. /resources/images/page/resource.xxx).
7. If you’re going to use the CMS, add the necessary folders and files (ala Microblog), plus make sure you add a Posts page and an Authors page to the structure you built in #5.
8. Design away with the Essentials add-on and the built-in Components. Some say start by getting all pages right for mobile first, then using breakpoint overrides to change design as the screen size goes up. Some of us do it the opposite way. But pick a direction! Get things right at the min or max size, then work your way to the other end.
9. Add your content to the Essentials and Components you used in #7 (I always start with the default lorem ipsum content because I’m worried about style first, content second, when designing a site. Likewise, add your beginning CMS content.
10. Do a complete and thorough Preview walk-thru of your site.

And throughout: file, folder, page, and resource names should be all lowercase, no spaces, hyphen-instead of space if you need it.&#x20;

### An Introduction to the Elements Interface

While the following video doesn’t cover every feature available in Elements, it offers a clear, high-level overview of the app’s layout and workflow. You’ll get a feel for how to add components to a page, how the editing interface is organized, and how to start building a website.

Think of this video as a quick tour to help you get comfortable with the basics. Once you’ve watched it, you’ll be ready to dive deeper and explore all the powerful options Elements has to offer.

{% embed url="https://youtu.be/zas7L3rMX18" %}

### Ready-Made Projects to Explore and Use

Elements has a large selection of free ready-made projects to choose from that are perfect for getting your website up and running quickly. Whether you want to launch something fast or learn by exploring how others have built their pages, these Projects are a great way to dive in and get inspired.

<figure><img src="../.gitbook/assets/CleanShot 2025-09-17 at 2 .50.18@2x.png" alt=""><figcaption></figcaption></figure>

### Optimize Media before import into Elements

It’s always a good idea to **prepare and optimize your media for the web** before importing it, especially large files like videos, audio, and high-res images. Uncompressed or oversized files can quickly inflate your project size and slow things down, both in the app and for your site visitors.

In general, we'd recommend:

* **Compressing images** using tools like Squash, TinyPNG or ImageOptim.
* **Optimizing videos** for the web using formats like MP4 (H.264) and reducing resolution/bitrate where possible.
* **Hosting larger files externally** (videos, audio, PDFs, etc.) and linking to them using URLs. That keeps your project lightweight and more manageable in the long run.

{% include "../.gitbook/includes/elements-website-hosting.md" %}
