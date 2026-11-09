---
description: Turn ?item=slug query strings into clean, readable URLs.
icon: map-location-dot
---

# Pretty URLs

Out of the box, the Elements CMS routes single-item pages with a query string:

```
mywebsite.com/blog/post/?item=my-first-post
```

This works, but it isn't pretty — and it isn't great for sharing or SEO. With a few small additions to your server config, you can rewrite those URLs into clean, readable paths:

```
mywebsite.com/blog/post/my-first-post
```

This page covers everything you need: the rewrite rules, the matching project setup inside Elements, and how to extend the same approach to tag and author pages.

### What you need

* An Apache web server with `mod_rewrite` enabled (this is the default on most shared hosts).
* SSH or FTP access to add a `.htaccess` file at the right level of your site.
* The **Pretty URLs** toggle enabled on the relevant components ([Collection](components/collection.md), [Item](components/item.md), [Search](components/search.md), [Tag List](components/tag-list.md)) — this tells them to write links in the clean form rather than the query-string form.

{% hint style="warning" %}
If your host runs Nginx, IIS, or LiteSpeed in non-Apache-compatibility mode, the `.htaccess` files below won't be read. The same rewrite logic still applies — see the [Nginx equivalent](#nginx-equivalent) at the bottom of this page.
{% endhint %}

### The two-part recipe

Pretty URLs need two things working together:

1. **A `.htaccess` file** that rewrites incoming requests like `/post/my-first-post` into the form the CMS understands (`/post/index.php?item=my-first-post`), and that issues 301 redirects from any old query-string links.
2. **A `<base href>` tag** in your project's template so that relative links on the rewritten page still resolve correctly.

Both pieces are simple. Together they make pretty URLs work transparently.

### Step 1 — Add the `.htaccess` file

Create a file called `.htaccess` in the root of your published site. If one already exists, add the rules below alongside what's there.

```apache
Options -MultiViews
RewriteEngine On

# 1. Redirect /post/?item=slug and /post/index.php?item=slug → /post/slug
RewriteCond %{THE_REQUEST} \s/+post/(?:index\.php)?\?item=([^\s&]+) [NC]
RewriteRule ^post/(?:index\.php)?$ /post/%1? [R=301,L,NE]

# 2. Don't rewrite if the request is for a real file or directory
RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]

# 3. Internally rewrite /post/slug → /post/index.php?item=slug
RewriteRule ^post/([^/]+)/?$ /post/index.php?item=$1 [L,QSA]
```

A line-by-line read:

* `Options -MultiViews` — disables Apache's content negotiation, which can interfere with rewrites that don't include a file extension.
* The first block (lines 4–5) catches any visitor or search-engine link that still uses the old `?item=slug` style and 301-redirects them to the clean form. This is what makes the change SEO-safe.
* The second block (lines 8–10) is a passthrough: if the request is for an existing file (an image, a CSS file, an actual HTML file), don't touch it.
* The third block (line 13) is the rewrite proper — it takes `/post/my-first-post` and serves the response from `/post/index.php?item=my-first-post`, transparently.

### Step 2 — Add the `<base href>` to your project template

Open your project's template in Elements and add a `<base>` tag inside the `<head>` section.

If your site is published at the root of your domain:

```html
<base href="/">
```

If it's published in a subfolder (for example `/blog/`):

```html
<base href="/blog/">
```

The `<base>` tag tells the browser the root from which all relative URLs on the page should be resolved. Without it, an Item page served from `/post/my-first-post` will try to load CSS, images, and links relative to `/post/my-first-post/…` rather than `/`, and you'll see a cascade of 404s.

### Step 3 — Enable Pretty URLs on the components

Once the server-side rewrite is in place, switch on the **Pretty URLs** toggle inside the inspector for any component that produces links to single items, tags, or authors:

* [Collection](components/collection.md) — toggles how Collection entries link to their single-item page.
* [Search](components/search.md) — toggles how result links are written.
* [Tag List](components/tag-list.md) — toggles how each tag links to its tag page.

Without this toggle, the components will keep writing `?item=slug` links and the 301 redirect rule will do most of the heavy lifting — but every click will incur a redirect hop. Turning the toggle on means the links are clean from the first request.

### Adapting the rules to your folder names

The rewrite block above assumes your single-item page lives at `/post/`. If your folder is called something else — say `/article/` or `/recipe/` — replace every `post` in the rules with that name. Everything else stays the same.

If you have multiple item pages under different folders, repeat the block once per folder.

### Tag and author pages

If you're using the [Tag List](components/tag-list.md) or [Search](components/search.md) component, you can apply the same pattern to your tag and author pages. Assuming a tag page at `/tag/` and an author page at `/author/`:

```apache
# Tag pages
RewriteCond %{THE_REQUEST} \s/+tag/(?:index\.php)?\?item=([^\s&]+) [NC]
RewriteRule ^tag/(?:index\.php)?$ /tag/%1? [R=301,L,NE]
RewriteRule ^tag/([^/]+)/?$ /tag/index.php?item=$1 [L,QSA]

# Author pages
RewriteCond %{THE_REQUEST} \s/+author/(?:index\.php)?\?item=([^\s&]+) [NC]
RewriteRule ^author/(?:index\.php)?$ /author/%1? [R=301,L,NE]
RewriteRule ^author/([^/]+)/?$ /author/index.php?item=$1 [L,QSA]
```

These can sit alongside the post block in the same `.htaccess` file.

### Subfolder publishing

If your site is published into a subfolder rather than the domain root — for example `mywebsite.com/blog/` — make two adjustments:

1. Place the `.htaccess` file in the subfolder, not the domain root.
2. Set `<base href="/blog/">` in your template (matching whatever the subfolder is).

The rewrite rules themselves don't need to change, because Apache evaluates them relative to the directory the `.htaccess` lives in.

### Nginx equivalent

If your host uses Nginx, the same logic translates to a `location` block in your server config. Since you usually don't have access to edit Nginx config on shared hosting, this is most relevant on a VPS or managed cloud host.

```nginx
location /post/ {
    # 1. Redirect /post/?item=slug → /post/slug
    if ($args ~ "^item=([^&]+)") {
        set $slug $1;
        return 301 /post/$slug;
    }

    # 2. Internally rewrite /post/slug → /post/index.php?item=slug
    rewrite ^/post/([^/]+)/?$ /post/index.php?item=$1 last;
}
```

Repeat the block for any tag or author folders that need the same treatment.

### Troubleshooting

**The page now 404s where it used to work.**\
Most often this means `mod_rewrite` isn't enabled, or `AllowOverride` is set too restrictively for your `.htaccess` to be read. Ask your host to confirm both are enabled.

**Links work, but every page load goes through a redirect.**\
The Pretty URLs toggle is off on the component generating the links. Switch it on so the components write clean links directly.

**CSS, JS, or images break after enabling pretty URLs.**\
The `<base href>` tag is missing or doesn't match where the site is published. Set it to `/` for root, or `/yourfolder/` for subfolder publishing.

**Redirect loops.**\
Usually means the second rule (the internal rewrite) is matching too eagerly. Double-check that the regex matches the folder name exactly and that you have the `[L]` flag on the final rewrite line.

**Some servers see `MultiViews` errors.**\
Older Apache configurations enable `MultiViews` by default, which can shortcut a request for `/post/my-first-post` to the file `post.php` and skip the rewrite. The `Options -MultiViews` line at the top of the recipe disables it.
