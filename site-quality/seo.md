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
6. Use a sitemap, which Elements generates automatically

### llms.txt and AI Markdown

Agents look for a root `llms.txt` and optional Markdown twins of your pages.

* Add `llms.txt` at the site root: Page Manager → New File → rename to `llms.txt`. Publish and export include it like `robots.txt`.
* Ask the Assistant (or a connected MCP client) to write or update that file from your pages.
* Turn on **Generate AI Markdown for every page** in Project Settings → Advanced to publish `<page>.html.md` beside each HTML or PHP page on publish/export. Preview does not write these files. Turning the option off does not remove previously uploaded `.md` files.

### How to Set Image Alt Text

Alternative text helps users, search engines, and accessibility tools understand your images.

In Elements 3.0 and later, alt text for a Resource image is stored on the image resource and reused by every Image component that uses it:

1. Open **Resources** in the left sidebar.
2. Select the image.
3. Open the **Resource Info** panel.
4. Enter a concise description in **Alt Text**.

For Custom and CMS images, set **Alt** in the Image component instead. See [Image](../elements/components/image.md#alternative-text) for complete guidance.

#### Why Image Alt Text Matters

1\. **Improves Accessibility** – Alt text helps visually impaired users who rely on screen readers understand the content of an image.

2\. **Boosts Image SEO** – Search engines use alt text to understand and index images, helping them appear in Google Images search results.

3\. **Enhances Page Relevance** – Properly written alt text with relevant keywords can reinforce the topic of your page, improving rankings.

4\. **Provides Context if Images Don’t Load** – If an image fails to load, the alt text is displayed instead, ensuring users still get the intended information.

### Metadata and Open Graph

Elements offers a dedicated Metadata panel for setting per-page titles, descriptions, and common Open Graph tags for social sharing.

<figure><img src="https://3876014504-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FNy6AECEVH2p4eFDicpM1%2Fuploads%2FJNbnS5dATgKflcZK2zfa%2FCleanShot%202025-05-09%20at%208%E2%80%AF.42.25%402x.png?alt=media&#x26;token=90da88a9-d457-4701-ba72-3971d29b106f" alt="Page Inspector showing editable SEO title, description and social image metadata"><figcaption><p>Setting Metadata in Elements</p></figcaption></figure>

### Website SEO Checklist

Use this checklist before launching your website:

* [ ] **Set Your Browser Titles & Meta Descriptions**\
  Use the metadata panel for each page (**Project › Page › Metadata**) to add unique, descriptive titles and summaries.
* [ ] **Use Proper Headings (H1, H2, H3…)**\
  Use one H1 per page, then nest H2 and H3 headings in a logical order. Set these using the Heading component.
* [ ] **Image ALT Text**\
  Set alt text for every meaningful Resource image using **Alt Text** in its Resource Info panel. For Custom and CMS images, use the Image component’s **Alt** field.
* [ ] **Clean, Human-Friendly URLs**\
  Keep filenames and paths tidy: `/about`, `/contact`, `/services/web-design`, etc. This makes navigation easier for humans _and_ robots.
* [ ] **Sitemap, robots.txt & llms.txt**\
  Elements automatically generates `sitemap.xml`. You can create a `robots.txt` file by adding a plain-text file to the Page Manager. Add a root `llms.txt` the same way (or ask the Assistant), and optionally enable **Generate AI Markdown for every page** in Advanced.
* [ ] **Optimise Images & Media**\
  Compress images before importing them using an app such as Squash or ImageOptim. Faster pages provide a better experience for visitors.
* [ ] **Descriptive Anchor Text**\
  Use meaningful link text such as “Contact Us” instead of “Click here”.
* [ ] **Preview Often**\
  Use Elements’ live preview and built-in accessibility audit. You can also test the published URL with Google’s [Lighthouse tool](https://pagespeed.web.dev/).
