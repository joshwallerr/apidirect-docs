# LinkedIn Post Details

Get detailed information about a specific LinkedIn post including engagement metrics (likes, comments, shares), author details, images, and embedded links.

## Endpoint

```
GET /v1/linkedin/post
```

**Price:** $0.002 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | LinkedIn post URL (max 500 characters) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `url` | string | Canonical post URL |
| `text` | string | Full post text content |
| `date` | string | Publication date and time |
| `author` | string | Author name |
| `author_description` | string | Author description (e.g. follower count) |
| `author_image` | string | Author profile image URL |
| `author_url` | string | Author profile URL |
| `likes` | integer | Number of likes |
| `comments` | integer | Number of comments |
| `shares` | integer | Number of shares |
| `reactions` | object | Breakdown of reaction types and counts |
| `is_repost` | boolean | Whether the post is a repost |
| `images` | array | Array of image URLs attached to the post |
| `links` | array | Links embedded in the post |
| `urn` | string | LinkedIn URN identifier |
| `source` | string | `"LinkedIn"` |
| `domain` | string | `"linkedin.com"` |
| `sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/post?url=https://www.linkedin.com/feed/update/urn:li:activity:7219434359085252608" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/post",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "url": "https://www.linkedin.com/feed/update/urn:li:activity:7219434359085252608"
    }
)
print(response.json())
```

## Example Response

```json
{
  "url": "https://www.linkedin.com/feed/update/urn:li:activity:7219434359085252608",
  "text": "Excited to share our latest project on AI...",
  "date": "2024-07-15 10:30:00",
  "author": "Jane Smith",
  "author_description": "1,234 followers",
  "author_image": "https://media.licdn.com/...",
  "author_url": "https://www.linkedin.com/in/janesmith/",
  "likes": 142,
  "comments": 23,
  "shares": 8,
  "reactions": {
    "like": 100,
    "celebrate": 25,
    "support": 17
  },
  "is_repost": false,
  "images": [
    "https://media.licdn.com/..."
  ],
  "links": [],
  "urn": "urn:li:activity:7219434359085252608",
  "source": "LinkedIn",
  "domain": "linkedin.com",
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
```
