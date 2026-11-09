---
description: Trigger external workflows when content or users change in the Online CMS Editor.
icon: webhook
---

# Webhooks

Webhooks let the Online CMS Editor notify another service when content or users change. Use them to trigger a deployment, send a team notification, update a search index, start an automation, or connect the CMS to another part of your workflow.

Webhooks require Pro and are managed by owners in the Online CMS Editor.

### Add a webhook

1. Sign in to the Online CMS Editor as an owner.
2. Open **Webhooks**.
3. Click **Add Webhook**.
4. Enter the endpoint URL that should receive webhook requests.
5. Choose the events this endpoint should receive.
6. Click **Create Webhook**.
7. Copy the signing secret immediately and store it somewhere safe.

{% hint style="warning" %}
Webhook endpoint URLs must use HTTPS. The signing secret is only shown when the webhook is created.
{% endhint %}

### Choose events

Each webhook can listen for one or more events:

| Event | Fires when |
| --- | --- |
| `file.created` | A content file is created. |
| `file.updated` | A content file is updated, renamed, or restored from version history. |
| `file.deleted` | A content file is deleted. |
| `user.created` | A user account is created. |
| `user.updated` | A user account is updated. |
| `user.deleted` | A user account is deleted. |

Only selected events are sent to the endpoint.

### Receive webhook requests

When an event fires, the Online CMS Editor sends a JSON `POST` request to the endpoint URL.

Example payload:

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

File events include the content filename and folder index. User events include the user email, and `user.created` also includes the role.

Webhook requests include these headers:

```text
Content-Type: application/json
X-Webhook-Signature: sha256=abcdef...
User-Agent: ElementsCMS/1.0
```

The signature is an HMAC-SHA256 hash of the raw JSON request body using the webhook signing secret. Verify the signature before trusting the request.

### Manage webhooks

From the **Webhooks** page, you can:

* Enable or disable a webhook without deleting it.
* Edit the endpoint URL.
* Change the selected events.
* Delete a webhook.
* Review recent delivery attempts in the delivery log.
* Clear the delivery log.

### Delivery log

Each delivery is attempted once. The delivery log shows recent attempts with the event, endpoint URL, HTTP status, success or error state, and any connection error.

If an endpoint returns a non-2xx response or cannot be reached, the delivery is marked as an error. Webhooks are not retried automatically, so your receiving endpoint should handle duplicate or missed events safely.
