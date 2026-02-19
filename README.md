# API Direct Documentation

Official documentation for [API Direct](https://apidirect.io) — a pay-as-you-go social media API.

Search real-time data across LinkedIn, Twitter/X, Reddit, YouTube, Instagram, and web forums through a unified REST API.

**Base URL:** `https://api.apidirect.io`
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

| Endpoint | Price | Docs |
|----------|-------|------|
| LinkedIn Posts | $0.006/request | [linkedin-posts.md](endpoints/linkedin-posts.md) |
| Twitter Posts | $0.006/page | [twitter-posts.md](endpoints/twitter-posts.md) |
| Reddit Posts | $0.003/request | [reddit-posts.md](endpoints/reddit-posts.md) |
| Reddit Comments | $0.003/page | [reddit-comments.md](endpoints/reddit-comments.md) |
| YouTube Videos | $0.005/page | [youtube-videos.md](endpoints/youtube-videos.md) |
| Instagram Posts | $0.006/page | [instagram-posts.md](endpoints/instagram-posts.md) |
| Forum Posts | $0.008/request | [endpoints/forum-posts.md](endpoints/forum-posts.md) |

## Account

- [Pricing](account/pricing.md) — Pay-per-request model, free tier, trust levels
- [Spending Limits](account/spending-limits.md) — Daily and monthly caps
- [API Keys](account/api-keys.md) — Creating, revoking, and managing keys

---

## Quick Example

```bash
curl "https://api.apidirect.io/v1/reddit/posts?query=programming&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

```python
import requests

response = requests.get(
    "https://api.apidirect.io/v1/reddit/posts",
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
