# Elements MCP Server

{% hint style="danger" %}
This feature is in development and is **not yet available in public builds of Elements.**
{% endhint %}

Elements has a built-in MCP server with a range of tools that LLM's can use.



As the time of writing (July 2026), the following Mac applications have MCP support and can connect to the Elements MCP server:

* Claude Code (Anthropic)
* Codex (OpenAI)
* Cursor (Anysphere, Inc)
* Gemini (Google, only available in the US on the Ultra plan)
* LM Studio

### Elements MCP Server Preferences

To enbale the MCP server in Elements, open the Elements Preferences panel and select the MCP Server tab. Switch on the MCP server, and connect your preferred client.

<figure><img src="../../.gitbook/assets/CleanShot 2026-07-04 at 9 .07.55@2x.png" alt=""><figcaption></figcaption></figure>

### How to connect LM Studio to the Elements MCP server

LM Studio requires you to configure the MCP connection manually. The JSON configuration should look like the xample below. Ensure the port number "9712" matches the port number in the Elements MCP Preferences panel.

```
{
  "mcpServers": {
    "elements": {
      "url": "http://localhost:9712/mcp"
    }
  }
}
```

### FAQ:

<details>

<summary>Why does Claude Code drop the connection to the Elements MCP server?</summary>

As this is fairly new and evolving technology, we’re not entirely sure why Claude is doing this. However, in our testing connecting Cursor, Codex or any other client to the Elements MCP is rock solid with no dropout issues.

</details>

