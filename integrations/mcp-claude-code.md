# Claude Code

Use API Direct as an MCP server in Claude Code to search social media and news directly from your terminal.

## Setup

Run this command, replacing `YOUR_API_KEY` with your key from the [API Keys](https://apidirect.io/dashboard/keys) page:

```bash
claude mcp add --transport http apidirect https://apidirect.io/mcp?token=YOUR_API_KEY
```

That's it. Claude Code can now search LinkedIn, Twitter/X, Reddit, YouTube, Instagram, forums, and news articles.

## Usage

Ask Claude Code to search any supported platform. For example:

- "Search LinkedIn for posts about AI agents"
- "Find recent Reddit discussions about React Server Components"
- "Search Twitter for posts about the latest OpenAI release"
- "Find YouTube videos about MCP servers"
- "Search news for articles about climate policy"

Claude Code will automatically call the right tool and return results.

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
| `search_news` | Search news articles from thousands of sources |

## Removing the Server

```bash
claude mcp remove apidirect
```

## Troubleshooting

**"No API key provided"** — Make sure the `?token=` parameter is included in the URL.

**"Invalid API key"** — Double-check your API key in the [dashboard](https://apidirect.io/dashboard/keys). Keys start with `ak_live_`.

**"Rate limit exceeded"** — You've hit your plan's rate limit. Check your [usage](https://apidirect.io/dashboard) or upgrade your plan.
