---
description: Receive signed webhook payloads when CMS content changes.
icon: webhook
---

# Webhooks

When a content item changes, the CMS can `POST` a payload to a URL you choose. Writes through the REST API fire the same hooks as writes through the Online Editor.

### Configure subscriptions

Webhook subscriptions are managed in the Online Editor under **Webhooks**. The REST API exposes read-only webhook settings at `GET /cms/settings/webhooks`; webhook create, update, and delete are handled in the Online Editor.

### Events

| Event | Fires when |
| --- | --- |
| `file.created` | A new content file is written. |
| `file.updated` | An existing content file changes or a version is restored. |
| `file.deleted` | A content file is removed. |
| `user.created` | A user is created in the Online Editor. |

Each subscription carries the list of events it cares about. The CMS filters at dispatch time.

### Payload shape

```json
{
  "event": "file.updated",
  "timestamp": "2026-04-20T10:00:00Z",
  "data": {
    "filename": "2026-04-20-hello.md",
    "folder": 0
  }
}
```

The full item body is not included. Fetch it with the REST API if you need it.

### Signing

Each request includes an `X-Webhook-Signature` header:

```text
X-Webhook-Signature: sha256=abcdef...
```

The signature is an HMAC-SHA256 of the raw JSON body using the subscription secret. Verify the signature before trusting the payload.

### Retries

Each delivery is attempted once and logged in the Online Editor's webhook log. If your endpoint returns non-2xx or cannot be reached, the log entry is marked as an error.

### Idempotency

Use `event`, `timestamp`, and the resource identifier in `data` to make your webhook handler idempotent.
