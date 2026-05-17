# OpenClaw

Use API Direct as an MCP server in OpenClaw to search social media and news from your AI agent.

## Setup

Add API Direct as an MCP server using the OpenClaw CLI:

```bash
openclaw mcp set apidirect '{"url":"https://apidirect.io/mcp?token=YOUR_API_KEY"}'
```

Replace `YOUR_API_KEY` with your key from the [API Keys](https://apidirect.io/dashboard/keys) page.

Verify the server was added:

```bash
openclaw mcp list
```

You can also view the server details with:

```bash
openclaw mcp show apidirect
```

## Usage

Once connected, ask your OpenClaw agent to search any supported platform:

- "Search LinkedIn for posts about AI agents"
- "Find recent Reddit discussions about React Server Components"
- "Search Twitter for posts about the latest OpenAI release"

OpenClaw will discover and call the appropriate API Direct tool automatically.

## Available Tools

All API Direct endpoints are available as MCP tools. This includes search across LinkedIn, Twitter/X, Facebook, Reddit, YouTube, Instagram, TikTok, forums, and news — as well as platform-specific tools for Twitter user profiles, Facebook pages/groups, and more. See the [endpoint documentation](/docs/linkedin-posts) for the full list.

## Troubleshooting

**"No API key provided"** — Make sure the `?token=` parameter is included in the URL.

**"Invalid API key"** — Double-check your API key in the [dashboard](https://apidirect.io/dashboard/keys). Keys start with `ak_live_`.

**Tools not appearing** — Run `openclaw mcp show apidirect` to verify the server config. Make sure the URL is correct.

**Removing the server** — To remove and re-add, run `openclaw mcp unset apidirect` and then set it again.
