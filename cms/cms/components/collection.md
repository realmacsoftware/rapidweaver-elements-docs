---
description: Display a dynamic list of CMS items, perfect for blogs, projects, and more.
---

# Collection

The **Collection** component displays a group of CMS items on your page — blog posts, products, team members, case studies, anything you keep in a CMS folder. It acts as a dynamic list that automatically updates whenever you add, edit, or remove content.

You choose which folder to pull from, how items should be sorted and filtered, and which page to use as the single-item template. With pagination, RSS, sitemap, and layout controls all built in, the Collection is the workhorse component of any CMS-powered page.

Typical use cases:

* Listing blog posts or news articles.
* Showing team members or portfolio projects.
* Displaying a paginated list of products.
* Surfacing only the latest 3 featured posts on a homepage.

### Settings

The Collection's inspector is divided into five groups: Settings, Filters, Pagination, RSS & Sitemap, and the usual layout controls.

#### Settings group

The wiring that connects the Collection to your content. In the inspector, each setting appears as its own labelled section: a **section heading** (e.g. _Item Template_) tells you what the setting is for, and the **control beneath it** is the input you edit. Three of these settings use a **Page** picker (so their control is labelled "Page") and one uses a **Folder** picker — "Page" and "Folder" describe the *type* of picker, not the setting's name. Use the section heading to tell them apart.

| Section heading | Control | What it does |
| --- | --- | --- |
| **Collection** | Folder picker | Select the folder of content to display in the collection. This is the CMS folder the items are read from. **Required.** |
| **Item Template** | Page picker | Select the page used to display a single item. Each Collection entry links to this page with the item's slug appended — it typically hosts your [Item](item.md) component. |
| **Tag Page Template** | Page picker | Select the page used to display tag lists (posts filtered by a tag taken from the URL). |
| **Author Page Template** | Page picker | Select the page used to display author lists (posts filtered by an author taken from the URL). |
| **Pretty URLs** | Enable toggle | When on, links are written as `/post/my-slug` rather than `/post/?item=my-slug`. Requires an `.htaccess` rule — see [Pretty URLs](../pretty-urls.md). Default: off. |

{% hint style="info" %}
The three **Page** pickers look identical in the inspector (all labelled "Page"). Always go by the **section heading** above each one — _Item Template_, _Tag Page Template_, or _Author Page Template_ — to make sure you're setting the right one.
{% endhint %}

#### Filters group

How the Collection sorts and filters the items it finds.

**Sorting**

* **Order By** — `Date Published` (default), `Title`, or `File Name`.
* **Order Direction** — `Descending` (default) or `Ascending`. With Date Published descending, the newest items come first.

**Filters**

* **Status** — `Published` (default), `Draft`, or `All`. Items with `status: draft` in their frontmatter only appear when this is set to `Draft` or `All`.
* **Date** — `In the past` (default), `In the future`, or `All dates`. Future-dated posts are hidden until their date arrives, unless this is changed. Useful for both scheduled posts and event listings.
* **Tags** — `All` (default), `From URL`, or `Custom`.
  * `From URL` reads the tag from the page's URL (typical on a tag page that filters posts).
  * `Custom` reveals a **Custom Tags** field where you can list tags directly, comma-separated.
* **Author** — same three options as Tags, working the same way against the `author` frontmatter property.
* **Featured** — `Both` (default), `Only Featured`, or `Not Featured`. Reads the boolean `featured` property from frontmatter.

#### Pagination group

* **Items Per Page** — how many items to show per page. Default: `10`.
* **Offset** — skip this many items before pagination begins. Default: `0`. Useful when one Collection shows the latest 3 featured posts and a second Collection on the same page shows everything else starting at item 4.

To add navigation, drop a [Collection Pagination](collection-pagination.md) or [Load More](load-more.md) component into the Collection's After drop zone.

#### RSS & Sitemap group

The Collection can publish a feed and a sitemap of its items, regenerated automatically when content changes.

* **RSS** toggle, **Folder**, and **Filename** — when enabled, an RSS XML file is written into the chosen folder (default: the page's directory). Filename defaults to `feed.xml`.
* **Sitemap** toggle, **Folder**, and **Filename** — same shape as RSS. Filename defaults to `sitemap.xml`.

You can read the active feed and sitemap URLs from `{{collection.rssURL}}` and `{{collection.sitemapURL}}` (see [Available data](collection.md#available-data) below).

{% hint style="info" %}
Append `?regenerate_rss=1` or `?regenerate_sitemap=1` to the page's URL to force a rebuild. The CMS otherwise regenerates these files lazily as content changes.
{% endhint %}

#### Columns, rows, and layout

The usual Elements layout controls — columns, rows, gap, padding — for arranging items inside the Collection. The Repeating drop zone is where each item's template lives.

### Drop zones

A Collection has three places where you can put other components:

* **Before** — appears once, above the list. A natural home for a heading, a search box, or a Tag List.
* **Repeating** — the per-item template. Anything you place here is rendered once per item, with `{{item.*}}` references resolving to the current item.
* **After** — appears once, below the list. Where Pagination, Load More, and "Subscribe to RSS" prompts typically go.

### Available data

Inside a Collection, two sets of references are available:

**Item-scoped (inside the Repeating zone):**

* `{{item.title}}`, `{{item.body}}`, `{{item.date}}`, `{{item.author}}`, `{{item.tags}}`, `{{item.url}}`, `{{item.slug}}` — and any custom frontmatter properties.
* See [Template Data](../template-data.md) for the complete reference, including nested image data and related-data lookups.

**Collection-scoped (in any zone):**

* `{{collection.rssURL}}` — the URL of this Collection's RSS feed (when enabled). Drop into a Text or Link component to point readers at the feed.
* `{{collection.sitemapURL}}` — the URL of this Collection's sitemap (when enabled).

### RSS and sitemap

To enable an RSS feed for a Collection, open the **RSS & Sitemap** inspector group and switch on the RSS toggle. The Collection will write the feed to the folder you choose (or the page's own directory by default), and `{{collection.rssURL}}` will resolve to its location.

The same pattern applies to the sitemap toggle.

{% hint style="info" %}
If you need to force a rebuild of the XML files, append `?regenerate_rss=1` or `?regenerate_sitemap=1` to the URL of the page where the Collection lives.
{% endhint %}

A common pattern: put a Text component into the Collection's After zone with a link to `{{collection.rssURL}}` so subscribers can find the feed easily.

### Common pitfalls

**The Collection is empty on the live site.**\
Check the Folder, then the filters. Items with `status: draft` are hidden by default, and future-dated posts are filtered out by the Date filter unless you change it.

**The page renders forever or shows a 500 error.**\
Almost always a `.html` extension or a missing PHP extension. See [Troubleshooting](../../getting-started/troubleshooting/).

**Links go to the right page but with `?item=…` in the URL.**\
Either the Pretty URLs toggle is off, or the `.htaccess` rule isn't in place. See [Pretty URLs](../pretty-urls.md).

**RSS feed isn't updating after a publish.**\
Append `?regenerate_rss=1` to force a rebuild. If the issue persists, check the [Log Manager](../../getting-started/troubleshooting/log-manager.md) for write errors on the destination folder.
