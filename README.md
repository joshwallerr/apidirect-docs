# API Direct Documentation

Official documentation for [API Direct](https://apidirect.io) — a pay-as-you-go social media API.

Search real-time data across LinkedIn, Twitter/X, Facebook, Reddit, YouTube, Instagram, TikTok, and web forums through a unified REST API.

**Base URL:** `https://apidirect.io`

**Auth:** `X-API-Key` header

**Docs:** [apidirect.io/docs](https://apidirect.io/docs)

---

## Getting Started

- [Introduction](getting-started/introduction.md) — What is API Direct, supported platforms, key features
- [Quickstart](getting-started/quickstart.md) — Sign up, create a key, make your first request
- [Authentication](getting-started/authentication.md) — X-API-Key header, key format, error responses

## Core Concepts

- [Response Format](core-concepts/response-format.md) — Unified response shape, fields, platform-specific extras
- [Pagination](core-concepts/pagination.md) — `page` vs `pages` parameter patterns
- [Error Handling](core-concepts/error-handling.md) — Error codes, status codes, retry guidance
- [Rate Limits](core-concepts/rate-limits.md) — Concurrency limits, 429 responses, best practices

## Endpoints

### LinkedIn

| Endpoint | Price | Docs |
|----------|-------|------|
| Search Posts | $0.006/request | [linkedin-posts.md](endpoints/linkedin-posts.md) |
| Post Details | $0.006/request | [linkedin-post.md](endpoints/linkedin-post.md) |
| Company Details | $0.006/request | [linkedin-company.md](endpoints/linkedin-company.md) |
| Company Posts | $0.006/request | [linkedin-company-posts.md](endpoints/linkedin-company-posts.md) |

### Twitter/X

| Endpoint | Price | Docs |
|----------|-------|------|
| Search Posts | $0.006/page | [twitter-posts.md](endpoints/twitter-posts.md) |
| User Profile | $0.006/request | [twitter-user.md](endpoints/twitter-user.md) |
| User Tweets | $0.006/page | [twitter-user-tweets.md](endpoints/twitter-user-tweets.md) |
| User Followers | $0.006/page | [twitter-user-followers.md](endpoints/twitter-user-followers.md) |
| User Following | $0.006/page | [twitter-user-following.md](endpoints/twitter-user-following.md) |
| Verified Followers | $0.006/page | [twitter-user-verified-followers.md](endpoints/twitter-user-verified-followers.md) |
| User Replies | $0.006/page | [twitter-user-replies.md](endpoints/twitter-user-replies.md) |
| Tweet Details | $0.006/request | [twitter-tweet.md](endpoints/twitter-tweet.md) |
| Tweet Retweets | $0.006/page | [twitter-tweet-retweets.md](endpoints/twitter-tweet-retweets.md) |
| Tweet Quotes | $0.006/page | [twitter-tweet-quotes.md](endpoints/twitter-tweet-quotes.md) |
| Tweet Comments | $0.006/page | [twitter-tweet-comments.md](endpoints/twitter-tweet-comments.md) |
| Trends | $0.006/request | [twitter-trends.md](endpoints/twitter-trends.md) |

### Facebook

| Endpoint | Price | Docs |
|----------|-------|------|
| Page Details | $0.008/request | [facebook-page-details.md](endpoints/facebook-page-details.md) |
| Page Posts | $0.008/page | [facebook-page-posts.md](endpoints/facebook-page-posts.md) |
| Page Photos | $0.008/page | [facebook-page-photos.md](endpoints/facebook-page-photos.md) |
| Page Videos | $0.008/page | [facebook-page-videos.md](endpoints/facebook-page-videos.md) |
| Page Reels | $0.008/page | [facebook-page-reels.md](endpoints/facebook-page-reels.md) |
| Page Reviews | $0.008/page | [facebook-page-reviews.md](endpoints/facebook-page-reviews.md) |
| Group Details | $0.008/request | [facebook-group-details.md](endpoints/facebook-group-details.md) |
| Group Posts | $0.008/page | [facebook-group-posts.md](endpoints/facebook-group-posts.md) |
| Search Group Posts | $0.008/page | [facebook-group-search.md](endpoints/facebook-group-search.md) |
| Search Posts | $0.008/page | [facebook-search-posts.md](endpoints/facebook-search-posts.md) |
| Search Pages | $0.008/page | [facebook-search-pages.md](endpoints/facebook-search-pages.md) |
| Search Videos | $0.008/page | [facebook-search-videos.md](endpoints/facebook-search-videos.md) |

### Reddit

| Endpoint | Price | Docs |
|----------|-------|------|
| Search Posts | $0.003/request | [reddit-posts.md](endpoints/reddit-posts.md) |
| Search Comments | $0.003/page | [reddit-comments.md](endpoints/reddit-comments.md) |

### Other Platforms

| Endpoint | Price | Docs |
|----------|-------|------|
| YouTube Videos | $0.005/page | [youtube-videos.md](endpoints/youtube-videos.md) |
| Instagram Posts | $0.006/page | [instagram-posts.md](endpoints/instagram-posts.md) |
| TikTok Videos | $0.006/page | [tiktok-videos.md](endpoints/tiktok-videos.md) |
| Forum Posts | $0.008/request | [forum-posts.md](endpoints/forum-posts.md) |
| News Articles | $0.008/request | [news-articles.md](endpoints/news-articles.md) |

## Integrations (MCP)

- [Claude Code](integrations/mcp-claude-code.md) — Terminal setup via `claude mcp add`
- [Claude Desktop](integrations/mcp-claude-desktop.md) — Connectors or config file setup
- [ChatGPT](integrations/mcp-chatgpt.md) — Developer Mode setup
- [Cursor](integrations/mcp-cursor.md) — `.cursor/mcp.json` setup

## Account

- [Pricing](account/pricing.md) — Pay-per-request model, free tier, trust levels
- [Spending Limits](account/spending-limits.md) — Daily and monthly caps
- [API Keys](account/api-keys.md) — Creating, revoking, and managing keys

---

## Quick Example

```bash
curl "https://apidirect.io/v1/reddit/posts?query=programming&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "programming", "page": 1}
)
print(response.json())
```

## Links

- [Sign up](https://apidirect.io/signup) — Free, no credit card required
- [Dashboard](https://apidirect.io/dashboard) — Manage keys, view usage, set limits
- [Live docs](https://apidirect.io/docs) — Full documentation with navigation
- [LLM-friendly docs](https://apidirect.io/llms-full.txt) — All docs as a single text file
- [Support](mailto:support@apidirect.io)
