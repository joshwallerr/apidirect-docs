# Twitter User Replies

Get replies posted by a specific Twitter/X user. Returns the content of each reply along with engagement metrics. Supports pagination.

## Endpoint

```
GET /v1/twitter/user/replies
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | Yes | Twitter username (without @, max 50 characters) |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `replies` | array | Array of replies by the user |
| `replies[].title` | string | Tweet title (format: `@username on X`) |
| `replies[].url` | string | Direct link to the reply |
| `replies[].date` | string | Publication date and time |
| `replies[].author` | string | Twitter username |
| `replies[].source` | string | `"Twitter (X)"` |
| `replies[].domain` | string | `"x.com"` |
| `replies[].snippet` | string | Reply content text |
| `replies[].likes` | integer | Number of likes |
| `replies[].retweets` | integer | Number of retweets |
| `replies[].replies` | integer | Number of replies to this reply |
| `replies[].quotes` | integer | Number of quote tweets |
| `replies[].bookmarks` | integer | Number of bookmarks |
| `replies[].views` | integer/null | Number of views |
| `replies[].author_followers` | integer | Author's follower count |
| `replies[].author_verified` | boolean | Whether the author is verified |
| `replies[].lang` | string | Tweet language code |
| `replies[].is_reply` | boolean | `true` (all entries are replies) |
| `replies[].is_quote` | boolean | Whether the reply is also a quote tweet |
| `replies[].hashtags` | string[] | Hashtags used |
| `replies[].user_mentions` | string[] | Usernames mentioned |
| `replies[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `replies[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `replies[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `replies[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `replies[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `username` | string | Requested username |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/user/replies?username=elonmusk&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/user/replies",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "elonmusk", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "replies": [
    {
      "title": "@elonmusk on X",
      "url": "https://twitter.com/elonmusk/status/...",
      "date": "2024-03-01 15:20:00",
      "author": "elonmusk",
      "source": "Twitter (X)",
      "domain": "x.com",
      "snippet": "@user Indeed, that is correct",
      "likes": 5000,
      "retweets": 200,
      "replies": 300,
      "quotes": 50,
      "bookmarks": 100,
      "views": 500000,
      "author_followers": 235918920,
      "author_verified": true,
      "lang": "en",
      "is_reply": true,
      "is_quote": false,
      "hashtags": [],
      "user_mentions": ["user"],
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
  "username": "elonmusk",
  "pages": 1,
  "count": 20
}
```
