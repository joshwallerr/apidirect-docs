# Twitter Posts

Search Twitter/X posts by keyword. Returns tweet content, author username, URL, publication date, and engagement metrics (likes, retweets, replies, views, and more). Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/twitter/posts
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |
| `sort_by` | No | Sort order: `most_recent` or `relevance` (default: `most_recent`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching tweets |
| `posts[].title` | string | Tweet title (format: `@username on X`) |
| `posts[].url` | string | Direct link to the tweet |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Twitter username |
| `posts[].source` | string | `"Twitter (X)"` |
| `posts[].domain` | string | `"x.com"` |
| `posts[].snippet` | string | Tweet content text |
| `posts[].likes` | integer | Number of likes |
| `posts[].retweets` | integer | Number of retweets |
| `posts[].replies` | integer | Number of replies |
| `posts[].quotes` | integer | Number of quote tweets |
| `posts[].bookmarks` | integer | Number of bookmarks |
| `posts[].views` | integer/null | Number of views (`null` when unavailable) |
| `posts[].author_followers` | integer | Author's follower count |
| `posts[].author_verified` | boolean | Whether the author is verified (blue checkmark) |
| `posts[].lang` | string | Tweet language code (e.g., `"en"`) |
| `posts[].is_reply` | boolean | Whether the tweet is a reply |
| `posts[].is_quote` | boolean | Whether the tweet is a quote tweet |
| `posts[].hashtags` | string[] | Hashtags used in the tweet |
| `posts[].user_mentions` | string[] | Usernames mentioned in the tweet |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/posts?query=AI&pages=2&sort_by=most_recent" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "AI",
        "pages": 2,
        "sort_by": "most_recent"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "@username on X",
      "url": "https://twitter.com/username/status/...",
      "date": "2024-01-15 14:30:00",
      "author": "username",
      "source": "Twitter (X)",
      "domain": "x.com",
      "snippet": "Tweet content here...",
      "likes": 142,
      "retweets": 38,
      "replies": 12,
      "quotes": 5,
      "bookmarks": 23,
      "views": 18420,
      "author_followers": 5243,
      "author_verified": false,
      "lang": "en",
      "is_reply": false,
      "is_quote": false,
      "hashtags": ["AI", "MachineLearning"],
      "user_mentions": ["OpenAI"]
    }
  ],
  "pages": 2,
  "count": 40
}
```
