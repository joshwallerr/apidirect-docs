# LinkedIn Posts

Search LinkedIn posts and articles by keyword. Returns post content, author, publication date, and direct URL for each result.

## Endpoint

```
GET /v1/linkedin/posts
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `page` | No | Page number for pagination (default: 1) |
| `sort_by` | No | Sort order: `most_recent` or `relevance` (default: `most_recent`) |
| `get_sentiment` | No | Set to `true` to add AI sentiment analysis to each result. Adds +$0.001 per request to the cost. Returns `positive`, `negative`, or `neutral`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching posts |
| `posts[].title` | string | Post title (format: `@author on LinkedIn`) |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Author name |
| `posts[].source` | string | `"LinkedIn"` |
| `posts[].domain` | string | `"linkedin.com"` |
| `posts[].snippet` | string | Post content text |
| `posts[].sentiment` | string/null | Sentiment classification: `positive`, `negative`, or `neutral`. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `page` | integer | Current page number |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/posts?query=artificial%20intelligence&page=1&sort_by=most_recent" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "artificial intelligence",
        "page": 1,
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
      "title": "@John Doe on LinkedIn",
      "url": "https://linkedin.com/posts/...",
      "date": "2024-01-15 14:30:00",
      "author": "John Doe",
      "source": "LinkedIn",
      "domain": "linkedin.com",
      "snippet": "Exciting developments in artificial intelligence...",
      "sentiment": "positive"
    }
  ],
  "page": 1,
  "count": 10
}
```
