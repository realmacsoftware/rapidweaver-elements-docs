---
description: List, read, create, update, and delete CMS content items.
icon: file-lines
---

# Items

Content items live inside a collection. Each item is a Markdown file with YAML frontmatter on disk. The JSON REST API exposes that content as JSON.

### `GET /cms/collections/{collection}/items`

List items in a collection.

| Field | Value |
| --- | --- |
| Auth | Optional for same-server calls. Cross-origin clients should send a key. |
| Role | Any |

Query string:

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `per_page` | int | Site default | Page size. |
| `page` | int | `1` | 1-indexed page number. |
| `status` | `published`, `draft`, `all` | Route default | Filter by status. |
| `tags` | string | - | Filter by tag slug or comma-separated tags. |
| `author` | string | - | Filter by author. |
| `orderBy` | string | `date_published` | Sort field. |
| `direction` | `asc`, `desc` | `desc` | Sort direction. |
| `offset` | int | `0` | Skip this many items before pagination. |

Response:

```json
{
  "success": true,
  "data": [
    {
      "slug": "hello",
      "title": "Hello",
      "url": "/blog/hello",
      "canonicalUrl": "https://example.test/blog/hello",
      "date": "2026-04-20",
      "status": "published"
    }
  ],
  "meta": {
    "currentPage": 1,
    "lastPage": 3,
    "totalItems": 42,
    "perPage": 20,
    "has_prev": false,
    "has_next": true
  },
  "timestamp": "2026-04-20T10:00:00+00:00"
}
```

### `GET /cms/collections/{collection}/items/{slug}`

Read one item as rendered HTML plus metadata.

| Field | Value |
| --- | --- |
| Auth | Optional for same-server calls. Cross-origin clients should send a key. |
| Role | Any |

### `GET /cms/collections/{collection}/items/{slug}/raw`

Read the item's raw frontmatter and source Markdown body with no HTML rendering.

| Field | Value |
| --- | --- |
| Auth | Required |
| Role | Any API key user |

This is useful for headless edit UIs and migration tooling.

### `POST /cms/collections/{collection}/items`

Create an item.

| Field | Value |
| --- | --- |
| Auth | Required |
| Role | Any API key user |

Body:

```json
{
  "slug": "hello-from-rest",
  "date_prefix": true,
  "fm": {
    "title": "Hello from REST",
    "date": "2026-04-20",
    "status": "draft",
    "tags": ["intro"]
  },
  "body": "Markdown body here."
}
```

`slug` is optional when `fm.title` is present. `fm` becomes the item's YAML frontmatter. `body` is the Markdown body.

Response:

```json
{
  "filename": "2026-04-20-hello-from-rest.md",
  "folder": 0,
  "message": "File created."
}
```

### `PUT /cms/collections/{collection}/items/{slug}`

Update an item through the same editor save handler as `PATCH`.

| Field | Value |
| --- | --- |
| Auth | Required |
| Role | Any API key user |

### `PATCH /cms/collections/{collection}/items/{slug}`

Update an item through the same editor save handler as `PUT`.

| Field | Value |
| --- | --- |
| Auth | Required |
| Role | Any API key user |

Body:

```json
{
  "fm": {
    "title": "Hello from REST",
    "status": "published"
  },
  "body": "Updated Markdown body here."
}
```

Frontmatter fields in `fm` merge over the existing frontmatter. Always send the complete Markdown `body` you want to keep. Omitting `body` saves an empty body.

Response:

```json
{
  "filename": "2026-04-20-hello-from-rest.md",
  "folder": 0,
  "message": "File saved."
}
```

### `DELETE /cms/collections/{collection}/items/{slug}`

Delete an item.

| Field | Value |
| --- | --- |
| Auth | Required |
| Role | Any API key user |

Response:

```json
{ "ok": true, "message": "File deleted." }
```
