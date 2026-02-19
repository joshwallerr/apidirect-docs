# Introduction

API Direct is a pay-as-you-go social media API that lets you search real-time data across major platforms through a single, unified interface.

## Supported Platforms

- **LinkedIn** - Search posts and articles
- **Twitter / X** - Search tweets and threads
- **Reddit** - Search posts and comments
- **YouTube** - Search videos with date filters
- **Instagram** - Search posts by hashtag
- **Forums** - Search discussion boards and Q&A sites across the web

## Base URL

All API requests are made to:

```
https://api.apidirect.io
```

## Key Features

**Unified response format** - Every endpoint returns the same core fields: `title`, `url`, `date`, `author`, `source`, and `snippet`. This makes it easy to work with data from multiple platforms without writing platform-specific parsing logic.

**Pay per request** - No monthly subscriptions or commitments. You only pay for successful API calls, with prices starting at $0.003 per request.

**Free tier** - Every account gets 50 free requests per endpoint per month. No credit card required to get started.

**Real-time data** - Results are fetched in real-time when you make a request. Access posts from the last few seconds to several years ago.

**Simple authentication** - Authenticate with a single API key passed in the `X-API-Key` header.

## Next Steps

- Follow the [Quickstart](quickstart.md) guide to make your first API call
- Learn about [Authentication](authentication.md)
- Browse the [endpoint documentation](../endpoints/linkedin-posts.md) for detailed parameter and response references
