---
description: Upload media and files through the JSON REST API.
icon: upload
---

# Uploads

The JSON REST API uploads resources with `multipart/form-data`. Send file bytes as the `file` part and include `folder` or `subpath` as form fields.

Base64 JSON uploads and MCP upload tickets are not part of this REST API.

### Browser upload

```js
const form = new FormData();
form.append('folder', '0');
form.append('subpath', 'blog');
form.append('file', fileInput.files[0]);

const res = await fetch(`${base}/cms/resources`, {
    method: 'POST',
    headers: { Authorization: `Bearer ${key}` },
    body: form,
});

const uploaded = await res.json();
```

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

### Server-side upload

In Node.js, use `FormData` or your HTTP client's multipart helper:

```js
import { openAsBlob } from 'node:fs';

const form = new FormData();
form.append('folder', '0');
form.append('subpath', 'blog');
form.append('file', await openAsBlob('hero.jpg'), 'hero.jpg');

const res = await fetch(`${base}/cms/resources`, {
    method: 'POST',
    headers: { Authorization: `Bearer ${key}` },
    body: form,
});
```

### Server-side guards

The server enforces:

* Configured maximum upload size.
* Blocked executable PHP-style extensions.
* Valid resource folder paths.
* Subfolder writes only when the license allows resource subfolders.
* Sanitized filenames with a unique suffix to avoid collisions.

### Image resize hook

Licensed resource folders can resize images during upload. If the uploaded image is larger than the folder's configured maximum width or height, the CMS resizes the saved file in place.

JPEG and WebP output use the folder's `JPEG/WebP Quality (%)` setting. PNG output keeps transparency and is resized without lossy quality adjustment.
