# Instagram Posts

Search Instagram posts by hashtag. Returns post URL, author username, publication date, and caption snippet. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/instagram/posts
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Hashtag to search (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |
| `sort_by` | No | Sort order: `most_recent` or `relevance` (default: `most_recent`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching posts |
| `posts[].title` | string | Post title (format: `@username on Instagram`) |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Instagram username |
| `posts[].source` | string | `"Instagram"` |
| `posts[].snippet` | string | Post caption text |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://api.apidirect.io/v1/instagram/posts?query=technology&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://api.apidirect.io/v1/instagram/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "technology",
        "pages": 2
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "@instagramuser on Instagram",
      "url": "https://instagram.com/p/...",
      "date": "2024-01-15 14:30:00",
      "author": "instagramuser",
      "source": "Instagram",
      "snippet": "Post caption here..."
    }
  ],
  "pages": 2,
  "count": 24
}
```
