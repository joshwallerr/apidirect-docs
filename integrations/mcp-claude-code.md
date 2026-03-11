# Claude Code

Use API Direct as an MCP server in Claude Code to search social media and news directly from your terminal.

## Setup

Run this command, replacing `YOUR_API_KEY` with your key from the [API Keys](https://apidirect.io/dashboard/keys) page:

```bash
claude mcp add --transport http apidirect https://apidirect.io/mcp?token=YOUR_API_KEY
```

That's it. Claude Code can now search LinkedIn, Twitter/X, Facebook, Reddit, YouTube, Instagram, TikTok, forums, and news articles.

## Usage

Ask Claude Code to search any supported platform. For example:

- "Search LinkedIn for posts about AI agents"
- "Find recent Reddit discussions about React Server Components"
- "Search Twitter for posts about the latest OpenAI release"
- "Get @elonmusk's Twitter profile"
- "Show me the latest tweets from @OpenAI"
- "What's trending on Twitter right now?"
- "Find YouTube videos about MCP servers"
- "Search news for articles about climate policy"

Claude Code will automatically call the right tool and return results.

## Available Tools

All API Direct endpoints are available as MCP tools. This includes search across LinkedIn, Twitter/X, Facebook, Reddit, YouTube, Instagram, TikTok, forums, and news — as well as platform-specific tools for Twitter user profiles, Facebook pages/groups, and more. See the [endpoint documentation](/docs/linkedin-posts) for the full list.

## Removing the Server

```bash
claude mcp remove apidirect
```

## Troubleshooting

**"No API key provided"** — Make sure the `?token=` parameter is included in the URL.

**"Invalid API key"** — Double-check your API key in the [dashboard](https://apidirect.io/dashboard/keys). Keys start with `ak_live_`.

**"Rate limit exceeded"** — You've hit your plan's rate limit. Check your [usage](https://apidirect.io/dashboard) or upgrade your plan.
