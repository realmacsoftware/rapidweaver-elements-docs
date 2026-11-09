---
description: Upload, list, move, rename, and delete CMS resources.
icon: images
---

# Resources

Resources are uploaded media and files, such as images, PDFs, and videos, that CMS items can reference. They live in resource folders configured in the Online Editor.

### `GET /cms/resources`

List entries in a resource folder.

| Field | Value            |
| ----- | ---------------- |
| Auth  | Required         |
| Role  | Any API key user |

Query string:

| Name      | Type   | Description                             |
| --------- | ------ | --------------------------------------- |
| `folder`  | int    | Resource folder index. Defaults to `0`. |
| `subpath` | string | Optional subfolder to list.             |

Response:

```json
{
  "folder": { "index": 0, "label": "Uploads" },
  "subpath": "",
  "dirs": [
    { "name": "blog", "type": "dir" }
  ],
  "files": [
    {
      "name": "hero.jpg",
      "size": 120938,
      "url": "/assets/hero.jpg",
      "modified": 1714000000,
      "is_image": true
    }
  ],
  "license": { "valid": true }
}
```

### `POST /cms/resources`

Upload a file with `multipart/form-data`.

| Field | Value            |
| ----- | ---------------- |
| Auth  | Required         |
| Role  | Any API key user |

Form fields:

| Name      | Type   | Description                             |
| --------- | ------ | --------------------------------------- |
| `file`    | file   | Required uploaded file bytes.           |
| `folder`  | int    | Resource folder index. Defaults to `0`. |
| `subpath` | string | Optional destination subfolder.         |

The JSON API does not accept base64 resource uploads. See [Uploads](https://github.com/realmacsoftware/rapidweaver-elements-docs-cms/blob/main/json-api/guides/uploads.md) for worked examples.

Response:

```json
{
  "name": "hero-662d8c981a65c.jpg",
  "url": "/assets/blog/hero-662d8c981a65c.jpg",
  "size": 120938,
  "modified": 1714000000,
  "is_image": true
}
```

### `PATCH /cms/resources`

Rename or move a file.

| Field | Value            |
| ----- | ---------------- |
| Auth  | Required         |
| Role  | Any API key user |

Rename body:

```json
{
  "folder": 0,
  "subpath": "blog",
  "file": "hero.jpg",
  "newName": "hero-v2"
}
```

Move body:

```json
{
  "op": "move",
  "folder": 0,
  "subpath": "blog",
  "file": "hero.jpg",
  "dest_subpath": "archive",
  "new_filename": "hero-v2.jpg"
}
```

### `DELETE /cms/resources`

Delete a file.

| Field | Value            |
| ----- | ---------------- |
| Auth  | Required         |
| Role  | Any API key user |

Body:

```json
{ "folder": 0, "subpath": "blog", "file": "hero.jpg" }
```

### `POST /cms/resources/folders`

Create a subfolder inside a resource folder.

| Field | Value            |
| ----- | ---------------- |
| Auth  | Required         |
| Role  | Any API key user |

Body:

```json
{ "folder": 0, "subpath": "blog", "name": "2026" }
```
