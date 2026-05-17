# Facebook Page Reviews

Get reviews for a Facebook page by page ID. Returns review text, recommendation status, and author info. Supports fetching multiple pages in a single call.

## Endpoint

```
GET /v1/facebook/page/reviews
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `page_id` | Yes | Facebook page ID (get from page details or page ID endpoint) |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `reviews` | array | List of review objects |
| `reviews[].review_text` | string | Text content of the review |
| `reviews[].recommend` | boolean | Whether the reviewer recommends the page |
| `reviews[].author_name` | string | Name of the reviewer |
| `reviews[].author_url` | string | URL to the reviewer's profile |
| `reviews[].reactions_count` | integer | Number of reactions on the review |
| `reviews[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `reviews[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `reviews[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `reviews[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `reviews[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `count` | integer | Number of reviews returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/page/reviews?page_id=100063543614476" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/page/reviews",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"page_id": "100063543614476"}
)
print(response.json())
```

## Example Response

```json
{
  "reviews": [
    {
      "review_text": "Great customer service and fast response times. Highly recommend!",
      "recommend": true,
      "author_name": "Sarah Johnson",
      "author_url": "https://www.facebook.com/profile.php?id=100048392017456",
      "reactions_count": 12,
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
    },
    {
      "review_text": "Decent product but shipping took longer than expected.",
      "recommend": true,
      "author_name": "Michael Chen",
      "author_url": "https://www.facebook.com/profile.php?id=100039284710385",
      "reactions_count": 4,
      "sentiment": {
        "emotions": {
          "joy": 10,
          "trust": 30,
          "fear": 0,
          "surprise": 0,
          "sadness": 15,
          "disgust": 10,
          "anger": 20,
          "anticipation": 5
        },
        "dominant_emotion": "trust",
        "emotional_intensity": 4,
        "polarity": "neutral"
      }
    }
  ],
  "count": 2,
  "pages": 1
}
```
