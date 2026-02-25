# Cursor

Use API Direct as an MCP server in Cursor to search social media and news from your editor.

## Setup

Create or edit `.cursor/mcp.json` in your project root:

```json
{
  "mcpServers": {
    "apidirect": {
      "url": "https://apidirect.io/mcp?token=YOUR_API_KEY"
    }
  }
}
```

Replace `YOUR_API_KEY` with your key from the [API Keys](https://apidirect.io/dashboard/keys) page.

Cursor will detect the config automatically. You can also add this to your global Cursor settings to make it available in all projects.

## Usage

In Cursor's AI chat, ask it to search any supported platform:

- "Search LinkedIn for posts about AI agents"
- "Find recent Reddit discussions about React Server Components"
- "Search Twitter for posts about the latest OpenAI release"

Cursor will call the appropriate tool and return the results.

## Available Tools

| Tool | Description |
|------|------------|
| `search_linkedin` | Search LinkedIn posts |
| `search_twitter` | Search Twitter/X posts |
| `search_reddit` | Search Reddit posts |
| `search_reddit_comments` | Search Reddit comments |
| `search_youtube` | Search YouTube videos |
| `search_instagram` | Search Instagram posts by hashtag |
| `search_tiktok` | Search TikTok videos |
| `search_forums` | Search forum posts across the web |
| `search_news` | Search news articles from thousands of sources |

## Troubleshooting

**"No API key provided"** — Make sure the `?token=` parameter is included in the URL.

**"Invalid API key"** — Double-check your API key in the [dashboard](https://apidirect.io/dashboard/keys). Keys start with `ak_live_`.

**Tools not appearing** — Make sure `.cursor/mcp.json` is valid JSON. Restart Cursor if needed.

**Global config** — To enable API Direct across all projects, add the config to Cursor's global MCP settings instead of a project-level file.
