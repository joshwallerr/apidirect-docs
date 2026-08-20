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
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

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
| `posts[].upvotes` | integer | Net upvotes (upvotes minus downvotes). |
| `posts[].upvote_ratio` | number | Fraction of votes that are upvotes, between 0 and 1. |
| `posts[].comments` | integer | Number of comments on the post. |
| `posts[].crossposts` | integer | Number of times the post has been crossposted. |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
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
      "upvotes": 1247,
      "upvote_ratio": 0.96,
      "comments": 312,
      "crossposts": 4,
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
  "page": 1,
  "count": 20
}
```
