---
description: List content collections configured for the site.
icon: folder-tree
---

# Collections

A collection is a folder of content items, such as `content/blog`. The Online Editor lets owners declare the site's content collections.

### `GET /cms/collections`

List every collection on the site.

| Field | Value |
| --- | --- |
| Auth | Optional for same-server calls. Cross-origin clients should send a key. |
| Role | Any |

Response:

```json
{
  "success": true,
  "data": [
    { "index": 0, "label": "Blog", "slug": "blog", "path": "content/blog" },
    { "index": 1, "label": "Changelog", "slug": "changelog", "path": "content/changelog" }
  ],
  "count": 2,
  "timestamp": "2026-04-20T10:00:00+00:00"
}
```

Use `index` or `slug` as the `{collection}` URL parameter on downstream routes.
