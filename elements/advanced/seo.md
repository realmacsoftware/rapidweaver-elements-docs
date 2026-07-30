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

The following is a list of items that will help your website rank better in search engines:

1. Setting Browser Titles
2. Add Meta Descriptions
3. Structuring URLs (so they are human readable)
4. Use the correct Header Tags
5. Creating Alt Text for Images
6. Using a [Sitemap](sitemap.xml.md) (Elements generates this automatically)

### How to set Image Alt text

Image description is useful for users, search engines, and accessibility tools. It can be set for each image under the "Description" setting in the Image Component settings.

<figure><img src="../../.gitbook/assets/CleanShot 2025-03-06 at 10 .22.37@2x.png" alt="Image resource selected with its Description field highlighted in the Inspector"><figcaption><p>Setting an Image Description in Elements</p></figcaption></figure>

#### Setting image alt text is important for SEO because it:

1\. **Improves Accessibility** – Alt text helps visually impaired users who rely on screen readers understand the content of an image.

2\. **Boosts Image SEO** – Search engines use alt text to understand and index images, helping them appear in Google Images search results.

3\. **Enhances Page Relevance** – Properly written alt text with relevant keywords can reinforce the topic of your page, improving rankings.

4\. **Provides Context if Images Don’t Load** – If an image fails to load, the alt text is displayed instead, ensuring users still get the intended information.

### Metadata and Open Graph

Elements offers a dedicated Metadata panel for setting per-page titles, descriptions, and common Open Graph tags for social sharing.

<figure><img src="../../.gitbook/assets/CleanShot 2025-05-09 at 8 .42.25@2x.png" alt="Page Inspector showing editable SEO title, description and social image metadata"><figcaption><p>Setting Metadata in Elements</p></figcaption></figure>

### Website SEO Checklist

If you want to level-up your new Elements project for SEO, run through this checklist before you officially launch your new website:

* [ ] **Set Your Browser Titles & Meta Descriptions**\
  Use the metadata panel for each page (Project > Page > Metadata) to add unique, descriptive titles and summaries. Search engines love this stuff, and so do users!
* [ ] **Use Proper Headings (H1, H2, H3…)**\
  Structure your content with headings, one H1 per page, then nest H2s and H3s sensibly. You can set these using the Heading component.
* [ ] **Image ALT Text**\
  Don’t forget to set alt text for every image via the Image component’s “Description” field. It helps accessibility & image SEO.
* [ ] **Clean, Human-Friendly URLs**\
  Keep filenames and paths tidy: /about, /contact, /services/web-desing, etc. Makes things easier for humans _and_ robots!
* [ ] **Sitemap & robots.txt**\
  Elements automatically generates a sitemap.xml, and you can [create a robots.txt](robots.txt.md) by adding a plain text file (right-click in the page list, choose “New File”, rename it robots.txt, fill it in).
* [ ] **Optimise Images & Media**\
  Before importing, compress images (with Squash, ImageOptim, etc.). Fast loads = happy visitors _and_ rankings!
* [ ] **Descriptive Anchor Text**\
  When linking, use meaningful text (“Contact Us” > “Click here”).
* [ ] **Preview Often**\
  Use Elements’ live preview and built-in accessibility audit (and maybe even toss your site’s URL into Google’s [Lighthouse tool](https://pagespeed.web.dev/)) to spot issues early.
