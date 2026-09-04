---
description: Connect AI tools to your open Elements project using the built-in MCP server
---

# Elements MCP Server

The built-in Elements MCP (Model Context Protocol) server lets compatible AI tools work with the project you have open in Elements. You can connect clients such as **Cursor**, **Codex**, or **Claude Desktop**.

Keep Elements running with your project open while using a connected AI tool.

## Enable the MCP server

1. In Elements, open **Settings** to show the Preferences window.
2. Select **AI**, then **MCP Server**.
3. Turn on **Allow AI tools to interact with Elements**.
4. Use the copy button beside the connection URL to copy it for your AI client.

The full settings path is **Settings > AI > MCP Server**. The screenshot below shows the server enabled, with a green status indicator and the URL `http://localhost:9712/mcp`.

<figure><img src="../../.gitbook/assets/elements-mcp-server-preferences.png" alt="Elements Preferences showing AI > MCP Server, the enabled Allow AI tools to interact with Elements switch, the connection URL, and the Install in Claude Desktop button"><figcaption><p>Enable the MCP server and connect your AI client in Settings > AI > MCP Server.</p></figcaption></figure>

## Connect Claude Desktop

Elements includes a bundled extension so Claude Desktop can connect without manual configuration.

1. Enable the MCP server using the steps above.
2. In the **Claude Desktop** section, click **Install in Claude Desktop…**.
3. Follow the installation prompts in Claude Desktop.
4. Keep your Elements project open, then use Claude Desktop to work with it.

## Connect Codex, Cursor, or another MCP client

Copy the URL shown in **Settings > AI > MCP Server** and add it to your AI client's MCP server settings. Use the URL displayed in Elements, as the port may differ from the example below:

```text
http://localhost:9712/mcp
```

This is a local connection to Elements on your Mac. Your client needs to support connecting to a local HTTP MCP server. The exact setup steps depend on the client you use.

### LM Studio configuration example

For LM Studio, add an MCP server configuration like this. Replace the URL if Elements shows a different one.

```json
{
  "mcpServers": {
    "elements": {
      "url": "http://localhost:9712/mcp"
    }
  }
}
```

## Troubleshooting

If your AI client cannot connect or loses its connection:

* Check that Elements is running and a project is open.
* Check that **Allow AI tools to interact with Elements** is switched on.
* Check that the URL in your client matches the URL currently shown in Elements.
* Reconnect or restart the MCP connection in your AI client.

## Turn off the MCP server

Open **Settings > AI > MCP Server** and turn off **Allow AI tools to interact with Elements** to stop AI clients interacting with Elements through the server.

For help adding API keys to the built-in assistant, see [Elements AI Assistant](elements-ai-assistant.md).
