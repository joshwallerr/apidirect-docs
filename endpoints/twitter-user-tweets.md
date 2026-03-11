# Twitter User Tweets

Get tweets posted by a specific Twitter/X user. Returns tweet content, engagement metrics, and metadata. Supports pagination to fetch multiple pages of results.

## Endpoint

```
GET /v1/twitter/user/tweets
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | Yes | Twitter username (without @, max 50 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `tweets` | array | Array of tweets by the user |
| `tweets[].title` | string | Tweet title (format: `@username on X`) |
| `tweets[].url` | string | Direct link to the tweet |
| `tweets[].date` | string | Publication date and time |
| `tweets[].author` | string | Twitter username |
| `tweets[].source` | string | `"Twitter (X)"` |
| `tweets[].domain` | string | `"x.com"` |
| `tweets[].snippet` | string | Tweet content text |
| `tweets[].likes` | integer | Number of likes |
| `tweets[].retweets` | integer | Number of retweets |
| `tweets[].replies` | integer | Number of replies |
| `tweets[].quotes` | integer | Number of quote tweets |
| `tweets[].bookmarks` | integer | Number of bookmarks |
| `tweets[].views` | integer/null | Number of views |
| `tweets[].author_followers` | integer | Author's follower count |
| `tweets[].author_verified` | boolean | Whether the author is verified |
| `tweets[].lang` | string | Tweet language code |
| `tweets[].is_reply` | boolean | Whether the tweet is a reply |
| `tweets[].is_quote` | boolean | Whether the tweet is a quote tweet |
| `tweets[].hashtags` | string[] | Hashtags used in the tweet |
| `tweets[].user_mentions` | string[] | Usernames mentioned |
| `username` | string | Requested username |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/user/tweets?username=elonmusk&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/user/tweets",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "elonmusk", "pages": 2}
)
print(response.json())
```

## Example Response

```json
{
  "tweets": [
    {
      "title": "@elonmusk on X",
      "url": "https://twitter.com/elonmusk/status/...",
      "date": "2024-03-01 18:30:00",
      "author": "elonmusk",
      "source": "Twitter (X)",
      "domain": "x.com",
      "snippet": "Tweet content here...",
      "likes": 50000,
      "retweets": 8000,
      "replies": 12000,
      "quotes": 3000,
      "bookmarks": 2000,
      "views": 5000000,
      "author_followers": 235918920,
      "author_verified": true,
      "lang": "en",
      "is_reply": false,
      "is_quote": false,
      "hashtags": [],
      "user_mentions": []
    }
  ],
  "username": "elonmusk",
  "pages": 2,
  "count": 40
}
```
