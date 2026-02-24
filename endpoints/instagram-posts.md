# Instagram Posts

Search Instagram posts by keyword. Returns post content, engagement metrics (likes, comments, shares, views), author metadata, and publication date. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/instagram/posts
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching posts |
| `posts[].title` | string | Post title (format: `@username on Instagram`) |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Instagram username |
| `posts[].source` | string | `"Instagram"` |
| `posts[].domain` | string | `"instagram.com"` |
| `posts[].snippet` | string | Post caption text |
| `posts[].likes` | integer | Number of likes |
| `posts[].comments` | integer | Number of comments |
| `posts[].shares` | integer | Number of shares |
| `posts[].reposts` | integer | Number of reposts |
| `posts[].views` | integer/null | Number of views/plays (`null` for image posts) |
| `posts[].is_video` | boolean | Whether the post is a video |
| `posts[].media_type` | string | Post type (e.g., `"feed"`, `"clips"`) |
| `posts[].author_verified` | boolean | Whether the author is verified |
| `posts[].author_name` | string | Author's display name |
| `posts[].hashtags` | string[] | Hashtags used in the caption |
| `posts[].mentions` | string[] | Usernames mentioned in the caption |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/posts?query=technology&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "technology",
        "pages": 2
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "@mrbeast on Instagram",
      "url": "https://instagram.com/p/DSDh2qaEVmQ",
      "date": "2025-12-09 20:16:58",
      "author": "mrbeast",
      "source": "Instagram",
      "domain": "instagram.com",
      "snippet": "How Many People Does it Take to Pull a Plane w/ @saudi_airlines",
      "likes": 530176,
      "comments": 5608,
      "shares": 9536,
      "reposts": 4353,
      "views": 29667777,
      "is_video": true,
      "media_type": "clips",
      "author_verified": true,
      "author_name": "MrBeast",
      "hashtags": [],
      "mentions": ["saudi_airlines"]
    }
  ],
  "pages": 2,
  "count": 20
}
```
