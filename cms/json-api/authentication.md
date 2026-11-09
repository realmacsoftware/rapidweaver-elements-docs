---
description: Create API keys and authenticate JSON REST API requests.
icon: key
---

# Authentication and API Keys

Every authenticated route on the JSON REST API uses a Bearer key prefixed with `api_`.

{% hint style="info" %}
`api_` keys and `mcp_` tokens are separate. `api_...` keys authenticate the JSON REST API documented here. `mcp_...` tokens authenticate the [MCP server](../mcp/) used by AI agents. The two key families do not work interchangeably.
{% endhint %}

### How keys work

* Keys are created by an owner on the **API** page inside the Online Editor.
* The API page is available only when the site has a license with JSON API access.
* Each key is bound to a specific user account.
* Requests made with the key act as that user and inherit their role.
* The plaintext key is shown once at creation. The server stores only a hash.
* Revoking a key takes effect on the next request.

### Send the key

Preferred header:

```
Authorization: Bearer api_exampletoken000000000000
```

Fallback query string, for clients that cannot set custom headers:

```
https://example.test/api/cms/collections/blog/items?token=api_exampletoken000000000000
```

The header is preferred because query strings can appear in browser history, server logs, analytics, and shared screenshots.

### Test a key

```sh
curl -i \
  -H "Authorization: Bearer api_exampletoken000000000000" \
  https://example.test/api/cms/
```

Expected: `200 OK` with a JSON body describing the API.

### Wrong key family

Using an `mcp_...` token against the JSON API returns `401 Unauthorized` with a message explaining that MCP tokens belong to the [MCP endpoint](../mcp/), not the JSON REST API.

### Status codes

| Code  | Meaning                                                              | Typical fix                                                                                                                                 |
| ----- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `200` | OK                                                                   | No action needed.                                                                                                                           |
| `401` | No key, invalid key, or wrong key family.                            | Generate an `api_...` key on the Online Editor's API page.                                                                                  |
| `402` | No active license with JSON API access.                              | Activate an existing Pro license or purchase Pro from **Workspace > License**. |
| `403` | The key is valid, but the bound user lacks the role for this action. | Use a key bound to a user with the required role.                                                                                           |
| `404` | Collection, item, or resource does not exist.                        | Check the URL and collection slug.                                                                                                          |
| `409` | Resource rename or move conflict.                                    | Choose a different target name or destination.                                                                                              |

See [Errors](errors.md) for the full response envelope and troubleshooting checklist.

### Rotate or revoke keys

To rotate a key, create a new one, deploy it to clients, then revoke the old one. To revoke a key, open the Online Editor's **API** page and delete it from the key list.
