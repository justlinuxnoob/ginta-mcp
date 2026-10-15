# Installing the Ginta MCP server (for AI agents)

Ginta is a **remote** MCP server. Do not clone, build or run anything.

1. Add this entry to the MCP settings file (for Cline: `cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "ginta": {
      "type": "streamableHttp",
      "url": "https://ginta.app/mcp"
    }
  }
}
```

2. There is no API key and no environment variable. The server uses OAuth: on the first tool call the client opens a Ginta sign-in page in the browser. Ask the user to sign in (or create a free account) and press **Allow**.

3. If the client cannot do OAuth for remote servers, use this entry instead (needs Node.js):

```json
{
  "mcpServers": {
    "ginta": { "command": "npx", "args": ["-y", "mcp-remote", "https://ginta.app/mcp"] }
  }
}
```

4. Check it works: call `list_sites`. Then call `get_guide` before building a website.

Before `create_site` or `update_site`, tell the user: "Building your website, this takes about 1–3 minutes."
