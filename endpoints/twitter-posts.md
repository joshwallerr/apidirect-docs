# Twitter Posts

Search Twitter/X posts by keyword. Returns tweet content, author username, URL, and publication date. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/twitter/posts
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |
| `sort_by` | No | Sort order: `most_recent` or `relevance` (default: `most_recent`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching tweets |
| `posts[].title` | string | Tweet title (format: `@username on X`) |
| `posts[].url` | string | Direct link to the tweet |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Twitter username |
| `posts[].source` | string | `"Twitter (X)"` |
| `posts[].domain` | string | `"x.com"` |
| `posts[].snippet` | string | Tweet content text |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/posts?query=AI&pages=2&sort_by=most_recent" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "AI",
        "pages": 2,
        "sort_by": "most_recent"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "@username on X",
      "url": "https://twitter.com/username/status/...",
      "date": "2024-01-15 14:30:00",
      "author": "username",
      "source": "Twitter (X)",
      "domain": "x.com",
      "snippet": "Tweet content here..."
    }
  ],
  "pages": 2,
  "count": 40
}
```
