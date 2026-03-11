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
      "user_mentions": []
    }
  ],
  "tweet_id": "1631781099415257088",
  "pages": 1,
  "count": 20
}
```
