# Reddit Comments

Search Reddit comments by keyword. Returns comment content, parent post URL, subreddit, author, and publication date. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/reddit/comments
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-5 (default: 1) |
| `sort_by` | No | Sort order: `most_recent`, `relevance`, or `top` (default: `most_recent`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching comments |
| `posts[].title` | string | Comment title (format: `u/username on r/subreddit`) |
| `posts[].url` | string | Link to the parent post |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Reddit username |
| `posts[].source` | string | `"Reddit (Comment)"` |
| `posts[].subreddit` | string | Subreddit name |
| `posts[].snippet` | string | Comment content text |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://api.apidirect.io/v1/reddit/comments?query=python&pages=2&sort_by=relevance" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://api.apidirect.io/v1/reddit/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "python",
        "pages": 2,
        "sort_by": "relevance"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "u/username on r/python",
      "url": "https://reddit.com/r/python/comments/...",
      "date": "2024-01-15 14:30:00",
      "author": "commenter",
      "source": "Reddit (Comment)",
      "subreddit": "python",
      "snippet": "Comment content..."
    }
  ],
  "pages": 2,
  "count": 50
}
```
