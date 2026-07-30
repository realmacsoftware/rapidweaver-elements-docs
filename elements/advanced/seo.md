---
description: All the essential SEO tools are built into Elements
icon: bullseye
---

# SEO

Elements gives you full control over the essential SEO tools and metadata needed to help your site get discovered.

You can define semantic HTML tags for structural elements (such as \<header>, \<section>, \<article>, and more), and set appropriate heading levels (\<h1>, \<h2>, \<p>, etc.) for text content. Image alt text is fully supported, ensuring accessibility and better indexing by search engines.

Elements automatically generates an XML sitemap for your project, and includes a dedicated Metadata panel for setting per-page titles, descriptions, and common Open Graph tags for social sharing.

For advanced users, Elements also provides direct access to the raw HTML template—perfect for inserting custom SEO tags or scripts not available through the UI.

### SEO Testing Tools

You can test the SEO performance of your website with the following tools:

* [Google Search Console](https://search.google.com/search-console/about) – submit sitemaps, monitor indexing, and spot issues
* [Lighthouse](https://developers.google.com/web/tools/lighthouse) – audit SEO basics from Chrome
* [Ahrefs Webmaster Tools](https://ahrefs.com/webmaster-tools) – free tools for basic SEO analysis

### Good SEO Practices in Elements

The following practices can help search engines understand and index your website:

1. Set browser titles
2. Add meta descriptions
3. Structure URLs so they are easy to read
4. Use the correct heading tags
5. Add alt text to images
6. Use a [sitemap](sitemap.xml.md), which Elements generates automatically

### How to Set Image Alt Text

Image descriptions help users, search engines and accessibility tools understand your content. Set them using the **Description** control in the Image component.

<figure><img src="../../.gitbook/assets/CleanShot 2025-03-06 at 10 .22.37@2x.png" alt="Image resource selected with its Description field highlighted in the Inspector"><figcaption><p>Setting an Image Description in Elements</p></figcaption></figure>

#### Why Image Alt Text Matters

1\. **Improves Accessibility** – Alt text helps visually impaired users who rely on screen readers understand the content of an image.

2\. **Boosts Image SEO** – Search engines use alt text to understand and index images, helping them appear in Google Images search results.

3\. **Enhances Page Relevance** – Properly written alt text with relevant keywords can reinforce the topic of your page, improving rankings.

4\. **Provides Context if Images Don’t Load** – If an image fails to load, the alt text is displayed instead, ensuring users still get the intended information.

### Metadata and Open Graph

Elements offers a dedicated Metadata panel for setting per-page titles, descriptions, and common Open Graph tags for social sharing.

<figure><img src="../../.gitbook/assets/CleanShot 2025-05-09 at 8 .42.25@2x.png" alt="Page Inspector showing editable SEO title, description and social image metadata"><figcaption><p>Setting Metadata in Elements</p></figcaption></figure>

### Website SEO Checklist

Use this checklist before launching your website:

* [ ] **Set Your Browser Titles & Meta Descriptions**\
  Use the metadata panel for each page (**Project › Page › Metadata**) to add unique, descriptive titles and summaries.
* [ ] **Use Proper Headings (H1, H2, H3…)**\
  Use one H1 per page, then nest H2 and H3 headings in a logical order. Set these using the Heading component.
* [ ] **Image ALT Text**\
  Set alt text for every meaningful image using the Image component’s **Description** field. This improves accessibility and image SEO.
* [ ] **Clean, Human-Friendly URLs**\
  Keep filenames and paths tidy: `/about`, `/contact`, `/services/web-design`, etc. This makes navigation easier for humans _and_ robots.
* [ ] **Sitemap & robots.txt**\
  Elements automatically generates `sitemap.xml`. You can [create a `robots.txt` file](robots.txt.md) by adding a plain-text file to the Page Manager.
* [ ] **Optimise Images & Media**\
  Compress images before importing them using an app such as Squash or ImageOptim. Faster pages provide a better experience for visitors.
* [ ] **Descriptive Anchor Text**\
  Use meaningful link text such as “Contact Us” instead of “Click here”.
* [ ] **Preview Often**\
  Use Elements’ live preview and built-in accessibility audit. You can also test the published URL with Google’s [Lighthouse tool](https://pagespeed.web.dev/).
