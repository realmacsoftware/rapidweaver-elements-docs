---
description: JSON REST API response envelopes, status codes, and troubleshooting.
icon: triangle-exclamation
---

# Errors

### Response envelopes

Public read routes and status routes use this success envelope:

```json
{
  "success": true,
  "data": { },
  "meta": { },
  "timestamp": "2026-04-20T10:00:00+00:00"
}
```

`meta` appears on paginated routes. `count` appears on some list routes.

Authenticated write and settings routes bridge into the Online Editor handlers. Those responses are still JSON, but they use the editor shape directly:

```json
{ "filename": "2026-04-20-hello.md", "folder": 0, "message": "File saved." }
{ "error": "File not found." }
{ "ok": true, "message": "File deleted." }
```

Envelope failures look like this:

```json
{
  "success": false,
  "error": "Key not found.",
  "code": 404,
  "timestamp": "2026-04-20T10:00:00+00:00"
}
```

For envelope failures, the HTTP status matches `code`. Editor-bridged failures set the HTTP status and return an `error` string without a `code` field.

### Status codes

| Code  | Meaning          | When                                                                 | Fix                                                                                                                                         |
| ----- | ---------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `200` | OK               | Success.                                                             | No action needed.                                                                                                                           |
| `400` | Bad Request      | Required field missing, malformed JSON, wrong shape.                 | Read `error` and fix the request.                                                                                                           |
| `401` | Unauthorized     | No key, invalid key, or wrong key family.                            | Send a valid `api_...` key.                                                                                                                 |
| `402` | Payment Required | Site has no active license with JSON API access.                     | Activate an existing Pro license or purchase Pro from **Workspace > License**. |
| `403` | Forbidden        | Same-server origin check failed or the user lacks the required role. | Send a key or use a key bound to a higher-role user.                                                                                        |
| `404` | Not Found        | Collection, item, or resource does not exist.                        | Check the slug, filename, or collection identifier.                                                                                         |
| `409` | Conflict         | Resource rename or move target already exists.                       | Choose a new name or destination.                                                                                                           |
| `500` | Server Error     | Handler crashed.                                                     | Check the web server's PHP error log.                                                                                                       |

### Troubleshooting checklist

1. **Always getting 402?** The site has no valid license with JSON API access. Check **License** in the Online Editor.
2. **Always getting 401?** Confirm the header is `Authorization: Bearer api_...`. If the key starts with `mcp_`, create a JSON API key instead.
3. **Getting 403?** The key's bound user may not have the required role or feature access.
4. **Getting 404 on an item that exists?** Items stored as `2026-04-20-hello.md` are addressable as either `hello` or the full filename. Compare against the slugified form.
5. **POST or PUT says fields are missing?** Set `Content-Type: application/json` for JSON item writes. Use `multipart/form-data` only for resource uploads.
6. **CORS preflight failing?** The API handles `OPTIONS` automatically. Cross-origin clients should send a key.

When reporting a bug, include the request URL, method, redacted headers, full response body, PHP version, and license status.
