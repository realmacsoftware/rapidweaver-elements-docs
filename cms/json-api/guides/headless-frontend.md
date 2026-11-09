---
description: Build a static site, SPA, or frontend app against the CMS API.
icon: window
---

# Headless Frontend

Use the JSON REST API when you want a frontend to read CMS content over HTTPS instead of rendering through Elements components directly.

### Do you need a key?

For public reads served from the same origin as the CMS, you do not need a key. The same-server origin check handles access.

For cross-origin reads, send an `api_...` key. Bind it to a dedicated integration user so you can revoke it later without disrupting editors.

{% hint style="warning" %}
The whole API requires active JSON API access. If access expires, every call returns `402 Payment Required`.
{% endhint %}

### Environment

```sh
CMS_BASE=https://example.test/api
CMS_KEY=api_exampletoken000000000000
```

Omit `CMS_KEY` for same-origin public reads.

### List posts

```js
const base = process.env.CMS_BASE;
const key = process.env.CMS_KEY;

async function listPosts({ page = 1, perPage = 20 } = {}) {
    const url = new URL(`${base}/cms/collections/blog/items`);
    url.searchParams.set('page', page);
    url.searchParams.set('per_page', perPage);

    const res = await fetch(url, {
        headers: key ? { Authorization: `Bearer ${key}` } : {},
    });

    if (!res.ok) throw new Error(`CMS ${res.status}`);

    const body = await res.json();
    return { items: body.data, meta: body.meta };
}
```

### Pagination

Paginated routes return a `meta` object with:

* `currentPage`
* `lastPage`
* `totalItems`
* `perPage`
* `has_prev`
* `has_next`

The API does not return next-page URLs. Build those links in your frontend.

### Tag pages

```js
async function postsWithTag(tag, { limit = 50 } = {}) {
    const url = new URL(`${base}/cms/tags/${encodeURIComponent(tag)}/items`);
    url.searchParams.set('content_path', '/absolute/path/to/content/blog');
    url.searchParams.set('per_page', limit);

    const res = await fetch(url, {
        headers: key ? { Authorization: `Bearer ${key}` } : {},
    });

    if (!res.ok) throw new Error(`CMS ${res.status}`);
    return (await res.json()).data;
}
```

### Render one post

```js
async function getPost(slug) {
    const res = await fetch(`${base}/cms/collections/blog/items/${slug}`, {
        headers: key ? { Authorization: `Bearer ${key}` } : {},
    });

    if (res.status === 404) return null;
    if (!res.ok) throw new Error(`CMS ${res.status}`);

    return (await res.json()).data;
}
```

The `data.body_html` field is the rendered HTML. `data.frontmatter` carries the YAML metadata.

### Client-side search

Pull the search index once per build, then feed it into MiniSearch, Fuse, or your preferred client-side search library:

```text
/cms/collections/search-index?collectionPath=content/blog
```

The response shape is tuned for client-side search, with fields such as `slug`, `title`, `url`, `canonicalUrl`, `excerpt`, `tags`, and `date`.

### Handle a license lapse

If JSON API access expires, calls return `402 Payment Required`. Detect this at the fetch boundary and show a clear error instead of silently rendering an empty page.

```js
if (res.status === 402) {
    throw new Error('CMS JSON API access is not active.');
}
```
