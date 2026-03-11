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
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |

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
      "user_mentions": ["user"]
    }
  ],
  "username": "elonmusk",
  "pages": 1,
  "count": 20
}
```
