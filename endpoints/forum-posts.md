# Forum Posts

Search forum posts across discussion boards, Q&A sites, and community forums. Returns post title, URL, source domain, and content snippet. Supports filtering by time period and country.

## Endpoint

```
GET /v1/forums/posts
```

**Price:** $0.008 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `page` | No | Page number, 1-10 (default: 1). 10 posts per page |
| `time` | No | Time filter: `any`, `hour`, `day`, `week`, `month`, `year` (default: `any`) |
| `country` | No | ISO 3166-1 alpha-2 country code (e.g., `US`, `GB`, `DE`) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching forum posts |
| `posts[].position` | integer | Result ranking position |
| `posts[].rank` | integer | Result rank value |
| `posts[].title` | string | Post or thread title |
| `posts[].url` | string | Direct link to the post |
| `posts[].source` | string | Source name or forum domain |
| `posts[].domain` | string | Forum domain name |
| `posts[].snippet` | string | Post content preview |
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
curl "https://apidirect.io/v1/forums/posts?query=programming&time=week&country=US" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/forums/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "programming",
        "time": "week",
        "country": "US"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "position": 1,
      "rank": 1,
      "title": "Discussion about programming",
      "url": "https://forum.example.com/thread/...",
      "source": "forum.example.com",
      "domain": "forum.example.com",
      "snippet": "Forum post content...",
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
  "count": 10
}
```
