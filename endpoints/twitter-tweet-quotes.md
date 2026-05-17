# Twitter Tweet Quotes

Get the quote tweets for a specific tweet. Returns the full content and engagement metrics for each quote tweet. Supports pagination.

## Endpoint

```
GET /v1/twitter/tweet/quotes
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `tweet_id` | Yes | Numeric tweet ID |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `quotes` | array | Array of quote tweets |
| `quotes[].title` | string | Tweet title (format: `@username on X`) |
| `quotes[].url` | string | Direct link to the quote tweet |
| `quotes[].date` | string | Publication date and time |
| `quotes[].author` | string | Twitter username of the quoter |
| `quotes[].source` | string | `"Twitter (X)"` |
| `quotes[].domain` | string | `"x.com"` |
| `quotes[].snippet` | string | Quote tweet content |
| `quotes[].likes` | integer | Number of likes |
| `quotes[].retweets` | integer | Number of retweets |
| `quotes[].replies` | integer | Number of replies |
| `quotes[].quotes` | integer | Number of quote tweets |
| `quotes[].bookmarks` | integer | Number of bookmarks |
| `quotes[].views` | integer/null | Number of views |
| `quotes[].author_followers` | integer | Quoter's follower count |
| `quotes[].author_verified` | boolean | Whether the quoter is verified |
| `quotes[].lang` | string | Tweet language code |
| `quotes[].is_reply` | boolean | Whether it is also a reply |
| `quotes[].is_quote` | boolean | Always `true` for this endpoint |
| `quotes[].hashtags` | string[] | Hashtags used |
| `quotes[].user_mentions` | string[] | Usernames mentioned |
| `quotes[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `quotes[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `quotes[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `quotes[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `quotes[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `tweet_id` | string | Requested tweet ID |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/tweet/quotes?tweet_id=1631781099415257088&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/tweet/quotes",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"tweet_id": "1631781099415257088", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "quotes": [
    {
      "title": "@quoter on X",
      "url": "https://twitter.com/quoter/status/...",
      "date": "2024-01-16 10:00:00",
      "author": "quoter",
      "source": "Twitter (X)",
      "domain": "x.com",
      "snippet": "This is so true! Great point here.",
      "likes": 200,
      "retweets": 50,
      "replies": 10,
      "quotes": 2,
      "bookmarks": 30,
      "views": 15000,
      "author_followers": 8000,
      "author_verified": false,
      "lang": "en",
      "is_reply": false,
      "is_quote": true,
      "hashtags": [],
      "user_mentions": [],
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
  "tweet_id": "1631781099415257088",
  "pages": 1,
  "count": 20
}
```
