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
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching comments |
| `posts[].title` | string | Comment title (format: `username on subreddit`) |
| `posts[].url` | string | Link to the parent post |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Reddit username |
| `posts[].source` | string | `"Reddit (Comment)"` |
| `posts[].domain` | string | `"reddit.com"` |
| `posts[].subreddit` | string | Subreddit name |
| `posts[].snippet` | string | Comment content text |
| `posts[].type` | string | `"comment"` |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/comments?query=python&pages=2&sort_by=relevance" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/comments",
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
      "title": "commenter on python",
      "url": "https://reddit.com/r/python/comments/...",
      "date": "2024-01-15 14:30:00",
      "author": "commenter",
      "source": "Reddit (Comment)",
      "domain": "reddit.com",
      "subreddit": "python",
      "snippet": "Comment content...",
      "type": "comment",
      "sentiment": {
        "emotions": {
          "joy": 40,
          "trust": 55,
          "fear": 0,
          "surprise": 10,
          "sadness": 0,
          "disgust": 0,
          "anger": 0,
          "anticipation": 30
        },
        "dominant_emotion": "trust",
        "emotional_intensity": 5,
        "polarity": "positive"
      }
    }
  ],
  "pages": 2,
  "count": 50
}
```
