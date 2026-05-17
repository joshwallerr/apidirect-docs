# LinkedIn Company Posts

Get recent posts from a LinkedIn company page by URL. Returns post content, engagement metrics (likes, comments, shares, reaction breakdowns), author info, images, videos, and pagination info.

## Endpoint

```
GET /v1/linkedin/company/posts
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | LinkedIn company page URL (max 500 characters) |
| `page` | No | Page number for pagination (default: 1) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of company posts |
| `posts[].url` | string | Post URL |
| `posts[].text` | string | Full post text content |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Author name |
| `posts[].author_description` | string | Author description |
| `posts[].author_image` | string | Author profile image URL |
| `posts[].author_url` | string | Author profile URL |
| `posts[].likes` | integer | Number of likes |
| `posts[].comments` | integer | Number of comments |
| `posts[].shares` | integer | Number of shares |
| `posts[].reactions` | object | Breakdown of reaction types and counts |
| `posts[].is_repost` | boolean | Whether the post is a repost |
| `posts[].images` | array | Array of image URLs |
| `posts[].video` | object | Video data (thumbnail, duration) or null |
| `posts[].links` | array | Links embedded in the post |
| `posts[].urn` | string | LinkedIn URN identifier |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `page` | integer | Current page number |
| `count` | integer | Number of posts returned |
| `total` | integer | Total number of posts available |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/company/posts?url=https://www.linkedin.com/company/visualsoft-uk-ltd&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/company/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "url": "https://www.linkedin.com/company/visualsoft-uk-ltd",
        "page": 1
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "url": "https://www.linkedin.com/feed/update/urn:li:activity:7437505720176144385",
      "text": "Exciting news from our team...",
      "date": "2024-03-11 14:32:25",
      "author": "Visualsoft | Shopify Plus Partner",
      "author_description": "16,391 followers",
      "author_image": "https://media.licdn.com/...",
      "author_url": "https://www.linkedin.com/company/visualsoft-uk-ltd/posts",
      "likes": 13,
      "comments": 0,
      "shares": 5,
      "reactions": {
        "like": 10,
        "empathy": 3
      },
      "is_repost": false,
      "images": [],
      "video": {
        "thumbnail": "https://media.licdn.com/...",
        "duration": 102166
      },
      "links": ["https://www.linkedin.com/company/sportsshoes-com/"],
      "urn": "urn:li:activity:7437505720176144385",
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
  "count": 10,
  "total": 462
}
```
