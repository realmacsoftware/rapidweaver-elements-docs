---
description: Add an instant, client-side search box to your CMS-powered site.
---

# Search

The **Search** component adds a search input to your page that filters CMS content as the visitor types. Results are scored by relevance and rendered using a template you design with native Elements components.

Searches happen entirely in the browser. The first time a visitor focuses the input, the component fetches a small JSON index for the chosen collection and runs all subsequent queries against it locally — no round-trip to the server per keystroke.

### How it works

1. The component receives a folder of CMS content to index.
2. On first interaction, the browser fetches a JSON index that contains each item's title, body excerpt, tags, author, and URL.
3. As the visitor types, the component scores items by where the term appears (title hits beat body hits) and renders the top results into a template you've designed.
4. Each result links to the appropriate page — the single-item template for posts, your tag page for tags, your author page for authors.

### Settings

The inspector for the Search component is divided into a few groups.

#### Settings group

* **Folder** — the CMS folder to index (for example `posts/`). Required.
* **Item Template — Page** — the page that displays a single item. Result links for posts will point here.
* **Tag Page Template — Page** — the page that displays posts filtered by tag. Used when a result is a tag.
* **Author Page Template — Page** — the page that displays posts by an author. Used when a result is an author.
* **Pretty URLs** — when enabled, links are written as `/post/my-slug` instead of `/post/?item=my-slug`. Requires an `.htaccess` rule on your server. See [Pretty URLs](../pretty-urls.md).

#### Search group

* **Placeholder Text** — the placeholder shown inside the empty input. Default: `Search...`
* **Max Results** — the maximum number of results to render. Default: `20`.
* **Min Characters** — how many characters the visitor must type before searching begins. Default: `2`. Lower values feel snappier but trigger more renders.

The Input group exposes typography, padding, colours, and borders for the input field itself, matching the controls you'd find on a Form Input or similar component.

### Designing the result template

The Search component has a single drop zone called **Search Results**. Anything you place there becomes the per-result template — a card layout, for example, with a heading, an excerpt, and an image.

Use `{{item.*}}` references inside the drop zone the same way you would inside a Collection or Item:

* `{{item.title}}` — the item's title.
* `{{item.excerpt}}` — a short excerpt suitable for result snippets.
* `{{item.body}}` — the item's body (use sparingly — full bodies make for noisy results).
* `{{item.url}}` — the resolved link, ready for an `<a href>`.
* `{{item.tags}}` — comma-separated tag names.
* `{{item.author}}` — the author's name.
* `{{item.image}}` — the image URL (back-compat shorthand). Use `{{item.image.alt}}` for the alt text.

You can use any native Elements component in the template — Headings, Typography, Image, Link, Divider — and bind them to those references. The component will clone your template once per result.

### Result links and Pretty URLs

If you've enabled **Pretty URLs**, make sure your `.htaccess` matches the folder name you've chosen for posts, tags, and authors. Without the rewrite, links will appear to work but will show the raw `?item=slug` query string. See [Pretty URLs](../pretty-urls.md) for the rewrite rules and the required `<base href>` in your project template.

### Performance notes

The search index is generated on the server at request time and cached. For large sites, consider:

* Keeping `Min Characters` at 2 or 3 so the index isn't fetched until the visitor genuinely intends to search.
* Including an excerpt in your frontmatter (`excerpt: …`) so the index doesn't need to fall back to the full body.
* Lowering `Max Results` if your result template is heavy.

The browser-side scoring is very fast for typical site sizes (hundreds to low thousands of items). If you have tens of thousands of items, talk to us — that's a different shape of problem.

### Common issues

**The input renders but no results ever appear.**\
Check that the collection folder is set, the page extension is `.php`, and your browser's network tab shows a successful index fetch. The index URL ends in `searchIndexEndpoint` — a 404 or 500 there usually means the API isn't installed.

**Result links go to the wrong page (or back to the search page).**\
The Item Template, Tag Page Template, and Author Page Template need to be set explicitly. If a template is empty the component skips that result type rather than guessing.

**Tags or authors aren't appearing in results.**\
Tags and authors only appear if you have matching `tags/` or `authors/` folders alongside your posts. See [Template Data](../template-data.md) for how related lookups are wired up.
