# Twitter Tweet Comments

Get the comments (replies) on a specific tweet. Returns the full content and engagement metrics for each reply. Supports pagination.

## Endpoint

```
GET /v1/twitter/tweet/comments
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `tweet_id` | Yes | Numeric tweet ID |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `comments` | array | Array of reply tweets |
| `comments[].title` | string | Tweet title (format: `@username on X`) |
| `comments[].url` | string | Direct link to the reply |
| `comments[].date` | string | Publication date and time |
| `comments[].author` | string | Twitter username of the commenter |
| `comments[].source` | string | `"Twitter (X)"` |
| `comments[].domain` | string | `"x.com"` |
| `comments[].snippet` | string | Reply content text |
| `comments[].likes` | integer | Number of likes |
| `comments[].retweets` | integer | Number of retweets |
| `comments[].replies` | integer | Number of replies to this comment |
| `comments[].quotes` | integer | Number of quote tweets |
| `comments[].bookmarks` | integer | Number of bookmarks |
| `comments[].views` | integer/null | Number of views |
| `comments[].author_followers` | integer | Commenter's follower count |
| `comments[].author_verified` | boolean | Whether the commenter is verified |
| `comments[].lang` | string | Tweet language code |
| `comments[].is_reply` | boolean | Always `true` for this endpoint |
| `comments[].is_quote` | boolean | Whether the reply is also a quote |
| `comments[].hashtags` | string[] | Hashtags used |
| `comments[].user_mentions` | string[] | Usernames mentioned |
| `comments[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `comments[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `comments[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `comments[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `comments[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `tweet_id` | string | Requested tweet ID |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/tweet/comments?tweet_id=1631781099415257088&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/tweet/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"tweet_id": "1631781099415257088", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "comments": [
    {
      "title": "@commenter on X",
      "url": "https://twitter.com/commenter/status/...",
      "date": "2024-01-15 15:00:00",
      "author": "commenter",
      "source": "Twitter (X)",
      "domain": "x.com",
      "snippet": "@username Great post! Totally agree.",
      "likes": 50,
      "retweets": 5,
      "replies": 2,
      "quotes": 0,
      "bookmarks": 3,
      "views": 5000,
      "author_followers": 2500,
      "author_verified": false,
      "lang": "en",
      "is_reply": true,
      "is_quote": false,
      "hashtags": [],
      "user_mentions": ["username"],
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
