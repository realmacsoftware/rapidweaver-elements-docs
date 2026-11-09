---
description: Route index and conventions for the JSON REST API.
icon: list
---

# Reference

Complete route index for the Elements CMS JSON REST API.

### Conventions

* **Base URL:** `https://example.test/api`, or whatever the Online Editor's **API** page shows.
* Most routes live under `/cms/`.
* Requests and responses are `application/json` unless noted.
* Public read routes use the envelope documented in [Errors](../errors.md).
* Authenticated write and settings routes bridge into the Online Editor handlers and may return the editor JSON shape directly.
* JSON API access is required for every route. Without it, the API returns `402 Payment Required`.
* Authenticated routes require `Authorization: Bearer api_...`. See [Authentication and API Keys](../authentication.md).
* Public read routes can be called same-server without a key. Cross-origin clients should send an `api_...` key.

### Resource pages

* `GET /` and `GET /status` - service status and CMS app version.
* [Collections](collections.md) - list the site's content collections.
* [Items](items.md) - CRUD for content items inside a collection.
* [Resources](resources.md) - media and file management.
* [Versions](versions.md) - item revision metadata, reads, and restore routes.
* [Settings](settings.md) - theme, users, and webhooks.
* [Search and Feeds](search-and-feeds.md) - search index, tags, RSS, sitemap, and related items.

### Collection addressing

Routes that target a specific collection accept either the integer folder index or the case-insensitive label slug. These are equivalent:

```text
GET /cms/collections/0/items
GET /cms/collections/blog/items
```

Slugs come from the folder label, such as `Blog Posts` becoming `blog-posts`, or from the folder-path basename.

### Item addressing

Items are stored on disk as `YYYY-MM-DD-<slug>.md` or `<slug>.md`. Item routes accept either:

* The slug alone, for example `hello-from-rest`.
* The full filename, for example `2026-04-20-hello-from-rest.md`.

Use the bare slug unless you need to target a specific dated filename.
