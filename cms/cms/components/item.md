---
description: Display a single CMS item — the detail view that pairs with a Collection.
---

# Item

The **Item** component displays a single piece of CMS content on a page. Where a [Collection](collection.md) shows a list of posts, projects, or profiles, an Item shows _one_ of them in full — typically the page a reader lands on when they click a Collection entry.

A blog is the clearest example. Your `/blog/` page uses a Collection to list every post. Your `/blog/post/` page uses an Item to render whichever post matches the slug in the URL.

### How an Item picks its content

The Item component reads its content from the URL. When a visitor arrives at `/blog/post/my-first-post`, the Item looks for a Markdown file with the matching slug in the folder you've pointed it at and renders that file's frontmatter and body.

Under the hood, requests are routed through a query string like `?item=my-first-post`. With [Pretty URLs](../pretty-urls.md) enabled, that's hidden from the visitor — but if you ever inspect a raw request, that's what's happening.

{% hint style="info" %}
If no slug is supplied, or no matching file is found, the Item component renders nothing. This is a good place to add a fallback message in your page's design — for example a Text component placed _outside_ the Item that says "Sorry, we couldn't find that post."
{% endhint %}

### Where to place an Item

Drop the Item component onto the page that should serve as your detail view. A typical setup looks like this:

* `/blog/` — a page containing a [Collection](collection.md) of posts.
* `/blog/post/` — a page containing an Item, configured to read from the same `posts/` folder.

The Collection's settings include a "Single item page" option that points at your Item page. When a visitor clicks an entry in the Collection, they're taken to the Item page with the matching slug.

{% hint style="warning" %}
The page hosting the Item component must use a `.php` extension. If it's set to `.html`, the CMS won't run and the page will be blank or show source code. See [System Requirements](../../getting-started/system-requirements.md).
{% endhint %}

### Drop zones

The Item component has three areas where you can place other components:

* **Before** — appears once, above the item's content. Useful for breadcrumbs, a "Back to blog" link, or a hero banner.
* **Repeating** — the main content area, rendered for the matched item. This is where you'd place a Heading bound to `{{item.title}}`, a Typography component bound to `{{item.body}}`, an author block, tags, and so on.
* **After** — appears once, below the item's content. A natural home for a [Related Items](related-items.md) component, comments embed, or a newsletter sign-up.

### Accessing the item's data

Any component placed inside an Item can read the current item's frontmatter and body using `{{item.*}}` references:

* `{{item.title}}` — the item's title.
* `{{item.body}}` — the rendered Markdown body.
* `{{item.date}}` — the publication date (use the `|date` filter to format it).
* `{{item.author}}` — the author, with related-data lookup if you have an `authors/` folder.
* `{{item.tags}}` — the array of tags, with related-data lookup if you have a `tags/` folder.
* `{{item.url}}` — the canonical URL for this item, useful for share links and `<link rel="canonical">`.
* `{{item.slug}}` — the URL-friendly portion of the filename.

For custom frontmatter properties, use the same pattern: `{{item.featured}}`, `{{item.category}}`, `{{item.price}}`, etc. The full reference lives in [Template Data](../template-data.md).

### A minimal Item page

Here's the bare bones of a single-post page, sketched as Twig you might place inside a custom template component:

```html
@raw()
<article>
    <header>
        <h1>{{item.title}}</h1>
        <p class="meta">
            {% if item.author %}By {{item.author.name|default(item.author)}} · {% endif %}
            {{item.date|date('F j, Y')}}
        </p>
    </header>

    {% if item.image %}
    <img src="{{item.image.src}}" alt="{{item.image.alt}}">
    {% endif %}

    <div class="prose">{{item.body}}</div>
</article>
@endraw
```

Most of the time you won't need raw Twig like this — you'll bind native Elements components (Heading, Typography, Image) to the same `{{item.*}}` references and let the design system do the styling for you.

### Common pitfalls

**The page is blank.**\
The page extension is probably `.html` instead of `.php`. See [System Requirements](../../getting-started/system-requirements.md).

**The page renders, but no item content shows.**\
The slug in the URL doesn't match any file in the configured folder. Check the folder setting on the Item component, and confirm that the Markdown file's filename matches the slug exactly (lowercase, hyphenated).

**Links from my Collection go to `/blog/post/?item=slug` instead of `/blog/post/slug`.**\
That's working as designed — Pretty URLs need an `.htaccess` rule to rewrite the query-string form into a clean path. See [Pretty URLs](../pretty-urls.md).

**My images don't appear on the live site.**\
Filename casing is the usual culprit. Use lowercase filenames everywhere and reference them in lowercase in your Markdown. See [Embedding Media](../markdown/embedding-media.md).
