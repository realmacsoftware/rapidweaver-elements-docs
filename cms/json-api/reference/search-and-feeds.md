---
description: Search index, tags, RSS, sitemap, related items, and legacy public routes.
icon: magnifying-glass
---

# Search and Feeds

These read-only discovery surfaces were the original `/api/*` surface before authenticated write routes landed. They accept same-server requests without a key and cross-origin requests with a key.

{% hint style="warning" %}
These routes still require active JSON API access. Without it, they return `402 Payment Required`.
{% endhint %}

### Search index

#### `GET /cms/collections/search-index`

Return a client-side-search-friendly index of the site.

| Field | Value |
| --- | --- |
| Auth | Optional for same-server calls. Cross-origin clients should send a key. |
| Role | Any |

Query string:

| Name | Type | Description |
| --- | --- | --- |
| `collectionPath` | string | Required content folder path, usually relative to the site base path. |
| `resourcesPath` | string | Web path used to resolve resource URLs. |
| `page_path` | string | Page URL prefix for generated item URLs. |
| `tag_page_path` | string | Tag page URL prefix. |
| `author_page_path` | string | Author page URL prefix. |
| `site_url` | string | Canonical URL base. |
| `pretty_urls` | boolean string | Defaults to `true`. |

Response shape: an array of objects, one per item, with fields such as `slug`, `title`, `url`, `canonicalUrl`, `excerpt`, `tags`, and `date`. The shape is tuned to work with MiniSearch or Fuse.

### Tags

#### `GET /cms/tags`

List every tag in use across the site with item counts.

| Field | Value |
| --- | --- |
| Auth | Optional for same-server calls. Cross-origin clients should send a key. |
| Role | Any |

Query string:

| Name | Type | Description |
| --- | --- | --- |
| `content_path` | string | Required content folder path to scan. |
| `tag_page_path` | string | Tag page URL prefix. |
| `pretty_urls` | boolean string | Defaults to `true`. |

#### `GET /cms/tags/{tag}/items`

List items carrying a given tag.

| Field | Value |
| --- | --- |
| Auth | Optional for same-server calls. Cross-origin clients should send a key. |
| Role | Any |

Accepts `content_path` plus pagination query parameters: `page` and `per_page`.

### RSS and Atom

#### `GET /cms/collections/{collection}/rss`

Return an RSS 2.0 feed for a single collection as `application/rss+xml`.

| Field | Value |
| --- | --- |
| Auth | Optional for same-server calls. Cross-origin clients should send a key. |
| Role | Any |

Query string: `title`, `description`, `link`, and `limit`.

### Sitemap

#### `GET /cms/collections/{collection}/sitemap`

Return an XML sitemap for a single collection as `application/xml`.

| Field | Value |
| --- | --- |
| Auth | Optional for same-server calls. Cross-origin clients should send a key. |
| Role | Any |

Query string: `baseUrl` and `limit`.

For a site-wide sitemap, concatenate per-collection sitemaps or use a separate static generation step.

### Related items

#### `GET /cms/items/related`

Find items related to a given item by shared tags and simple content overlap.

| Field | Value |
| --- | --- |
| Auth | Optional for same-server calls. Cross-origin clients should send a key. |
| Role | Any |

Query string:

| Name | Type | Description |
| --- | --- | --- |
| `contentPath` | string | Required path to the source item file. |
| `by` | string | Comma-separated criteria. Defaults to `tags`. |
| `limit` | int | Defaults to `5`. |
| `page_path` | string | Page URL prefix for generated URLs. |
| `site_url` | string | Canonical URL base. |

### Legacy public item routes

These routes predate the collection slug routes and remain for compatibility with existing Elements components.

| Route | Notes |
| --- | --- |
| `GET\|POST /cms/collections/items` | List items for `collectionPath`; accepts the same listing query params as collection item lists. |
| `GET /cms/collections/items/{slug}` | Read one item from `collectionPath`. |
| `GET /cms/items/{slug}` | Search all discovered collections for one slug. |
