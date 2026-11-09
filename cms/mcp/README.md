---
description: Connect Claude, Cursor, and other AI assistants to the Online Editor with MCP.
icon: sparkles
---

# Overview and Setup

The Elements CMS Online Editor includes an MCP server for AI assistants that support the Model Context Protocol. Once connected, an assistant can browse your site's content, draft and publish posts, organise resources, restore versions, and manage supported settings through ordinary conversation.

{% hint style="warning" %}
**Pro / MCP access is required.** MCP requires an active Pro license for the site's domain with MCP access enabled. If access lapses, MCP tokens and OAuth clients stop working.
{% endhint %}

### What you can ask it to do

Once connected, talk to your AI assistant in plain English:

* _"Draft three blog post ideas based on my last ten posts."_
* _"What is in my drafts folder? Summarise each one in a sentence."_
* _"Rename every file in the press folder to start with `press-`."_
* _"Change the site's accent colour to a deeper blue."_
* _"Restore yesterday's post to the previous version."_

The assistant can only do what the connected user is allowed to do. A token bound to an editor can edit content, but cannot perform owner-only actions such as changing theme settings.

### Before you start

You need:

* Elements CMS v2 installed and published.
* An active license with MCP access registered to the site's domain.
* Owner access to the Online Editor, because only owners can create MCP tokens or download connection bundles.
* An MCP-compatible client, such as Claude Desktop, Claude on the web, Cursor, or MCP Inspector.

### Choose a connection method

| Method                         | Best for                                               | What you do                                                                  |
| ------------------------------ | ------------------------------------------------------ | ---------------------------------------------------------------------------- |
| **Download a `.mcpb` bundle**  | Claude Desktop                                         | Download a bundle from the Online Editor and double-click it.                |
| **Use a server URL and token** | Cursor, MCP Inspector, custom clients                  | Copy the endpoint URL, create an `mcp_...` token, and configure your client. |
| **OAuth sign-in**              | Claude on the web and clients that open a browser flow | Paste the endpoint URL and sign in through the Online Editor.                |

All three methods connect to the same MCP endpoint and act as the user you authorise.

### Method A: Claude Desktop bundle

This is the fastest way to connect Claude Desktop.

1. Sign in to the Online Editor as an owner.
2. Open **AI** > **Connections**.
3. Under **Claude Desktop**, click **Download for Claude Desktop**.
4. Give the bundle a name, choose the user the assistant should act as, and download it.
5. Double-click the downloaded `elements-cms-<your-host>.mcpb` file and confirm the install in Claude Desktop.
6. Start a new chat and ask: _"What tools do you have access to?"_

Each bundle download creates its own private MCP token. Removing the bundle from Claude Desktop does not revoke the server token, so revoke unused bundle tokens from **AI** > **Connections**.

{% embed url="https://www.youtube.com/watch?v=2-yVxnqkXIA&t=2s" %}

{% embed url="https://www.youtube.com/watch?v=Y1m3106Lnk0" %}

{% embed url="https://www.youtube.com/watch?v=m5IeJeWpLa0" %}

### Method B: Manual URL and token

Use this for clients that let you configure a custom MCP server URL.

#### 1. Copy the endpoint URL

In the Online Editor, open **AI** > **Connections**. The endpoint looks like:

```
https://example.test/editor/mcp.php
```

Use the exact URL shown in your editor.

#### 2. Create a token

Under **Connect any MCP client**, click **Create token**. Give it a clear name, choose the user the assistant should act as, and copy the plaintext token immediately. It starts with `mcp_` and is shown only once.

#### 3. Configure your client

Preferred header:

```
Authorization: Bearer mcp_exampletoken000000000000
```

Fallback URL, for clients that cannot set headers:

```
https://example.test/editor/mcp.php?token=mcp_exampletoken000000000000
```

{% hint style="warning" %}
Prefer the `Authorization` header. Tokens in URLs can appear in browser history, server logs, proxy logs, analytics, and screenshots.
{% endhint %}

#### Using the Endpoint URL and token in Codex

The [OpenAI Codex app](https://openai.com/codex/) supports this method, but the UI settings in Codex don't always seem to work. We'd recommend just asking Codex to set up the connection for you. Here's a video showing how this process works.

{% embed url="https://www.youtube.com/watch?v=9e9VQNJittA" %}

### Method C: OAuth sign-in

Some MCP clients can open a browser sign-in flow. In those clients, paste only the MCP endpoint URL:

```
https://example.test/editor/mcp.php
```

When the client connects, it opens the Online Editor sign-in page. After you authorise it, the CMS issues OAuth tokens to that client. You can see and revoke OAuth-connected apps under **AI** > **Connections**.

### Try your first prompt

After connecting, ask:

> _"What tools do you have access to?"_

The assistant should list tools such as `content_list_items`, `content_read_item`, `resources_upload_request`, and `settings_get_theme`. If it says it has no tools, check the endpoint URL, license status, and token or OAuth connection.

### What your AI can do

For the full list of tools and example prompts, see the [Tools Reference](tools.md).

| Area                    | What the assistant can do                                                                   |
| ----------------------- | ------------------------------------------------------------------------------------------- |
| **Content**             | List and create collections, read items, create drafts, update posts, and delete items.     |
| **Resources and media** | List, upload, rename, move, delete files, and create resource subfolders.                   |
| **Site settings**       | Read theme settings, update theme settings as an owner, list users, and list webhooks.      |
| **Version history**     | List versions, read a saved version, or restore an older version.                           |
| **MCP resources**       | Read browseable context such as `cms://site`, `cms://collections`, and collection listings. |

### API keys and MCP tokens

{% hint style="info" %}
`api_...` keys and `mcp_...` tokens are separate. `api_...` keys authenticate the [JSON REST API](../json-api/). `mcp_...` tokens authenticate the MCP server for AI assistants. They do not work interchangeably.
{% endhint %}

### Managing tokens and clients

On **AI** > **Connections**, you can see every active MCP token, the user it acts as, whether it came from a Claude Desktop bundle, and when it was last used. Revoke a token to disconnect any assistant using it.

Good habits:

* Create one token per client or device.
* Use descriptive names, such as `Claude Desktop - Home Mac`.
* Bind tokens to the lowest-privilege user that can do the job.
* Revoke tokens or OAuth clients you do not recognise.
* Revoke old tokens when a device, client, or person no longer needs access.

### Troubleshooting

| You see                                                            | What it means                                                                                                    | Fix                                                                                                |
| ------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `MCP access requires Pro plan for this domain`                     | The domain does not have active MCP access.                                                                      | Check the license in the Online Editor and activate or purchase Pro.                               |
| `Missing bearer token` or `Invalid bearer token`                   | The client did not send a token, the token was copied incorrectly, or it has been revoked.                       | Create a new token or download a fresh bundle, then reconnect.                                     |
| The assistant says it has no tools                                 | The URL may be wrong, the license may not include MCP access, or the client may have cached a failed connection. | Re-check the endpoint, confirm the license, then remove and re-add the MCP server in the client.   |
| The token's last-used timestamp never changes                      | The client is not reaching your CMS.                                                                             | Confirm the site is reachable over HTTPS and the endpoint URL is not truncated.                    |
| The assistant cannot do something the user should be allowed to do | The token may be bound to a lower-privilege user.                                                                | Check the token's user on **AI** > **Connections**, then recreate it for the right user if needed. |
| Claude Desktop shows that the extension failed to start            | Claude Desktop could not reach the site, or the bundle token was revoked.                                        | Confirm the site is reachable and download a new bundle if needed.                                 |
