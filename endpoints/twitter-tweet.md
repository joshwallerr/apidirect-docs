# Twitter Tweet Details

Get detailed information for a single tweet by its ID. Returns the full tweet content, engagement metrics, author info, and metadata.

## Endpoint

```
GET /v1/twitter/tweet
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `tweet_id` | Yes | Numeric tweet ID |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `tweet` | object | Tweet data |
| `tweet.title` | string | Tweet title (format: `@username on X`) |
| `tweet.url` | string | Direct link to the tweet |
| `tweet.date` | string | Publication date and time |
| `tweet.author` | string | Twitter username |
| `tweet.source` | string | `"Twitter (X)"` |
| `tweet.domain` | string | `"x.com"` |
| `tweet.snippet` | string | Tweet content text |
| `tweet.likes` | integer | Number of likes |
| `tweet.retweets` | integer | Number of retweets |
| `tweet.replies` | integer | Number of replies |
| `tweet.quotes` | integer | Number of quote tweets |
| `tweet.bookmarks` | integer | Number of bookmarks |
| `tweet.views` | integer/null | Number of views |
| `tweet.author_followers` | integer | Author's follower count |
| `tweet.author_verified` | boolean | Whether the author is verified |
| `tweet.lang` | string | Tweet language code |
| `tweet.is_reply` | boolean | Whether the tweet is a reply |
| `tweet.is_quote` | boolean | Whether the tweet is a quote tweet |
| `tweet.hashtags` | string[] | Hashtags used |
| `tweet.user_mentions` | string[] | Usernames mentioned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/tweet?tweet_id=1631781099415257088" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/tweet",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"tweet_id": "1631781099415257088"}
)
print(response.json())
```

## Example Response

```json
{
  "tweet": {
    "title": "@username on X",
    "url": "https://twitter.com/username/status/1631781099415257088",
    "date": "2024-01-15 14:30:00",
    "author": "username",
    "source": "Twitter (X)",
    "domain": "x.com",
    "snippet": "Full tweet content here...",
    "likes": 5000,
    "retweets": 1200,
    "replies": 300,
    "quotes": 150,
    "bookmarks": 800,
    "views": 250000,
    "author_followers": 50000,
    "author_verified": true,
    "lang": "en",
    "is_reply": false,
    "is_quote": false,
    "hashtags": ["tech"],
    "user_mentions": []
  }
}
```
