# Claude Desktop

Use API Direct as an MCP server in Claude Desktop to search social media from your conversations.

## Option 1: Connectors (Recommended)

1. Open Claude Desktop and go to **Settings** > **Connectors**
2. Click **Add custom connector**
3. Paste the following URL, replacing `YOUR_API_KEY` with your key from the [API Keys](https://apidirect.io/dashboard/keys) page:

```
https://apidirect.io/mcp?token=YOUR_API_KEY
```

4. Click **Add**

## Option 2: Config File

If you prefer manual configuration, add API Direct to your `claude_desktop_config.json`:

**macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`

**Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "apidirect": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://apidirect.io/mcp?token=YOUR_API_KEY"]
    }
  }
}
```

Replace `YOUR_API_KEY` with your key from the [API Keys](https://apidirect.io/dashboard/keys) page. Restart Claude Desktop after saving the file.

This option requires Node.js to be installed, as it uses `npx` to run the `mcp-remote` bridge.

## Usage

Once connected, ask Claude to search any supported platform:

- "Search LinkedIn for posts about AI agents"
- "Find recent Reddit discussions about React Server Components"
- "Search Twitter for posts about the latest OpenAI release"

Claude will ask for permission the first time it uses a tool, then return results inline.

## Available Tools

| Tool | Description |
|------|------------|
| `search_linkedin` | Search LinkedIn posts |
| `search_twitter` | Search Twitter/X posts |
| `search_reddit` | Search Reddit posts |
| `search_reddit_comments` | Search Reddit comments |
| `search_youtube` | Search YouTube videos |
| `search_instagram` | Search Instagram posts by hashtag |
| `search_forums` | Search forum posts across the web |

## Troubleshooting

**"No API key provided"** — Make sure the `?token=` parameter is included in the URL.

**"Invalid API key"** — Double-check your API key in the [dashboard](https://apidirect.io/dashboard/keys). Keys start with `ak_live_`.

**Tools not appearing** — Restart Claude Desktop after adding the connector or editing the config file.

**Config file option not working** — Make sure Node.js is installed (`node --version`). The `mcp-remote` package is fetched automatically via `npx`.
