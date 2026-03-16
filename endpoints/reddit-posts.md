# Reddit Posts

Search Reddit posts by keyword. Returns post title, URL, subreddit, author, and content snippet. Supports multiple sort options including hot and top posts.

## Endpoint

```
GET /v1/reddit/posts
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `page` | No | Page number, 1-5 (default: 1) |
| `sort_by` | No | Sort order: `most_recent`, `relevance`, `hot`, or `top` (default: `most_recent`) |
| `get_sentiment` | No | Set to `true` to add AI sentiment analysis to each result. Adds +$0.001 per request to the cost. Returns `positive`, `negative`, or `neutral`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching posts |
| `posts[].title` | string | Post title |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Reddit username |
| `posts[].source` | string | `"Reddit"` |
| `posts[].domain` | string | `"reddit.com"` |
| `posts[].subreddit` | string | Subreddit name |
| `posts[].snippet` | string | Post content text |
| `posts[].sentiment` | string/null | Sentiment classification: `positive`, `negative`, or `neutral`. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `page` | integer | Current page number |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/posts?query=programming&page=1&sort_by=hot" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "programming",
        "page": 1,
        "sort_by": "hot"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "Reddit post title",
      "url": "https://reddit.com/r/programming/...",
      "date": "2024-01-15 14:30:00",
      "author": "redditor",
      "source": "Reddit",
      "domain": "reddit.com",
      "subreddit": "programming",
      "snippet": "Post content...",
      "sentiment": "positive"
    }
  ],
  "page": 1,
  "count": 20
}
```
