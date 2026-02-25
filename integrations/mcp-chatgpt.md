# ChatGPT

Use API Direct as an MCP server in ChatGPT to search social media and news from your conversations.

Developer Mode is required (ChatGPT Pro, Team, Enterprise, or Edu).

## Setup

1. Open ChatGPT and go to **Settings** > **Apps**
2. Under **Advanced**, toggle **Developer Mode** on
3. Click **Create** and fill in:
   - **Name:** API Direct
   - **Server URL:** the URL below, with your API key from the [API Keys](https://apidirect.io/dashboard/keys) page:

```
https://apidirect.io/mcp?token=YOUR_API_KEY
```

4. Check **"I trust this provider"** and click **Create**

## Usage

Once the app is created, just ask ChatGPT to search any platform in a new conversation:

- "Search LinkedIn for posts about AI agents"
- "Find recent Reddit discussions about React Server Components"
- "Search Twitter for posts about the latest OpenAI release"

ChatGPT will automatically use the API Direct tools and display the results.

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

**Developer Mode not available** — Requires a ChatGPT Pro, Team, Enterprise, or Edu plan.
