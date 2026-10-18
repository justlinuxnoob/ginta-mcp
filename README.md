# [Ginta](https://ginta.app) MCP server

<p align="center"><a href="https://ginta.app"><img src="logo-400.png" width="120" alt="Ginta"></a></p>

**AI website maker with hosting, built-in forms and an MCP for Claude and ChatGPT.**

Build and host websites from Claude, ChatGPT or Claude Code. Your AI writes the site, Ginta publishes it live on `yourname.ginta.page` (or your own domain). Includes working forms, menus, bookings, blogs, an owner /admin, encrypted API keys and build uploads. OAuth sign-in, free tier.

This is a **hosted (remote) MCP server**. There is nothing to install, clone or build, and no API key goes in your config.

| | |
|---|---|
| Endpoint | `https://ginta.app/mcp` |
| Transport | Streamable HTTP |
| Auth | OAuth 2.1 (dynamic client registration). Metadata: `https://ginta.app/.well-known/oauth-protected-resource/mcp` |
| Official MCP Registry | `app.ginta/ginta` ([server.json](server.json)) |
| Website | https://ginta.app · docs: https://ginta.app/docs/ |
| Pricing | Free tier; paid plans from €5/month |

The first time you connect, a Ginta window opens: sign in or create a free account, then press **Allow**. Your websites are saved in that Ginta account.

## Connect

### Claude (claude.ai and the desktop app)

**Customize → Connectors → + → Add custom connector**. Name `Ginta`, URL `https://ginta.app/mcp`, leave the OAuth fields empty. Then **Connect** and sign in.

### ChatGPT

Turn on **Developer mode** (Settings → Apps & Connectors → Advanced settings), then **Create**: name `Ginta`, URL `https://ginta.app/mcp`, authentication **OAuth**.

### Claude Code

```bash
claude mcp add --transport http ginta https://ginta.app/mcp
```

Then run `/mcp`, choose **ginta → Authenticate** and sign in in your browser.

Or install it as a Claude Code plugin from this repository:

```bash
claude plugin marketplace add justlinuxnoob/ginta-mcp
```

```bash
claude plugin install ginta@ginta
```

### Gemini CLI

```bash
gemini extensions install https://github.com/justlinuxnoob/ginta-mcp
```

Then run `/mcp auth ginta` inside Gemini CLI and sign in in your browser. The extension is [`gemini-extension.json`](gemini-extension.json).

### Cline, Cursor and other clients

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

(Cursor uses `"url"` alone, without `"type"`.) One-click for Cursor: [Add Ginta to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=ginta&config=eyJ1cmwiOiJodHRwczovL2dpbnRhLmFwcC9tY3AifQ==); the same config is in [`.mcp.json`](.mcp.json). For a client that only runs local (stdio) servers, use [`mcp-remote`](https://www.npmjs.com/package/mcp-remote), which handles the OAuth sign-in:

```json
{
  "mcpServers": {
    "ginta": { "command": "npx", "args": ["-y", "mcp-remote", "https://ginta.app/mcp"] }
  }
}
```

## Tools

| Tool | What it does |
|---|---|
| `get_guide` | Ginta's design and building guide (the AI reads it first) |
| `list_sites` | Your websites, plan, limits and credits |
| `check_name` | Is `name.ginta.page` free? |
| `create_site` | Publish a new website (or get an upload link for a finished build) |
| `get_site` | Read a website's pages, images and history |
| `update_site` | Change a website with small edits |
| `upload_files` | Upload images, fonts or a whole build (.zip) |
| `restore_version` | Undo: bring back an earlier version |
| `preview_site` | Screenshots so the AI can check the design |
| `attach_image` | Put your own photo or logo online |
| `manage_site` | Rename a website, change its address, badge or form emails, mark messages read, delete |
| `get_messages` | Messages visitors sent through the website's forms |
| `get_stats` | Visitors, top pages, referrers, speed and SEO scores |
| `manage_module` | Ready-made parts: menu, bookings, shop, blog, gallery, events, quote requests, announcements |
| `manage_admins` | People who can sign in to the website's own `/admin` |
| `manage_secrets` | Store an API key for a website, encrypted and write-only |
| `manage_connections` | Let the website's code call an outside API with a stored key |
| `connect_domain` | Connect your own domain, with step-by-step DNS help |

## Try it

> Use Ginta to make a website for my bakery "Forno da Graça" in Lisbon. We bake sourdough and pastel de nata, open Tue–Sun 8–18.

## About this repository

This repository holds the public listing material for Ginta's MCP server: connection instructions, logo, the official registry's `server.json`, `.mcp.json` + `.claude-plugin/plugin.json` (Claude Code plugin), `.cursor-plugin/plugin.json` (Cursor, cursor.directory), `gemini-extension.json` (Gemini CLI) and `lhm.plugin.json` (LobeHub). The server itself is hosted by Ginta; its source code is not public. Support: support@ginta.app
