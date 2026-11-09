---
description: Walk through the core JSON REST API workflow in a few curl commands.
icon: bolt
---

# Quickstart

This walkthrough covers the most common JSON REST API operations using `curl`.

Assumptions:

* Your CMS is published at `https://example.test/`.
* JSON API access is active for the domain.
* You have an API key, for example `api_exampletoken000000000000`.
* You have a content collection called `blog`.

```sh
export BASE=https://example.test/api
export KEY=api_exampletoken000000000000
AUTH="Authorization: Bearer $KEY"
```

### 1. List collections

```sh
curl -H "$AUTH" "$BASE/cms/collections"
```

Response:

```json
{
  "success": true,
  "data": [
    { "index": 0, "label": "Blog", "slug": "blog", "path": "content/blog" }
  ],
  "timestamp": "2026-04-20T10:00:00+00:00"
}
```

Use either `slug` or `index` in downstream URLs.

### 2. List items

```sh
curl -H "$AUTH" "$BASE/cms/collections/blog/items"
```

Use query parameters such as `status`, `page`, and `per_page` to filter and paginate the list.

### 3. Create an item

```sh
curl -X POST -H "$AUTH" -H "Content-Type: application/json" \
  -d '{
        "slug": "hello-from-rest",
        "fm": {
          "title": "Hello from REST",
          "status": "draft"
        },
        "body": "This was created via the JSON API."
      }' \
  "$BASE/cms/collections/blog/items"
```

Response:

```json
{
  "filename": "2026-04-20-hello-from-rest.md",
  "folder": 0,
  "message": "File created."
}
```

### 4. Read the raw item, then update it

```sh
curl -H "$AUTH" "$BASE/cms/collections/blog/items/hello-from-rest/raw"
```

Use the returned `body` when saving. The save handler merges frontmatter fields, but replaces the Markdown body with the `body` value you send.

```sh
curl -X PATCH -H "$AUTH" -H "Content-Type: application/json" \
  -d '{
        "fm": { "status": "published" },
        "body": "This was created via the JSON API."
      }' \
  "$BASE/cms/collections/blog/items/hello-from-rest"
```

`PATCH` and `PUT` both use the editor save handler.

### 5. Delete an item

```sh
curl -X DELETE -H "$AUTH" \
  "$BASE/cms/collections/blog/items/hello-from-rest"
```

Response:

```json
{ "ok": true, "message": "File deleted." }
```

From here, browse the [Reference](reference/), read the [Headless Frontend](https://github.com/realmacsoftware/rapidweaver-elements-docs-cms/blob/main/json-api/guides/headless-frontend.md) guide, or use [Content Migration](https://github.com/realmacsoftware/rapidweaver-elements-docs-cms/blob/main/json-api/guides/content-migration.md) for bulk imports.
