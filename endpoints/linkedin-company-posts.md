# LinkedIn Company Posts

Get recent posts from a LinkedIn company page by URL. Returns post content, engagement metrics (likes, comments, shares, reaction breakdowns), author info, images, videos, and pagination info.

## Endpoint

```
GET /v1/linkedin/company/posts
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | LinkedIn company page URL (max 500 characters) |
| `page` | No | Page number for pagination (default: 1) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of company posts |
| `posts[].url` | string | Post URL |
| `posts[].text` | string | Full post text content |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Author name |
| `posts[].author_description` | string | Author description |
| `posts[].author_image` | string | Author profile image URL |
| `posts[].author_url` | string | Author profile URL |
| `posts[].likes` | integer | Number of likes |
| `posts[].comments` | integer | Number of comments |
| `posts[].shares` | integer | Number of shares |
| `posts[].reactions` | object | Breakdown of reaction types and counts |
| `posts[].is_repost` | boolean | Whether the post is a repost |
| `posts[].images` | array | Array of image URLs |
| `posts[].video` | object | Video data (thumbnail, duration) or null |
| `posts[].links` | array | Links embedded in the post |
| `posts[].urn` | string | LinkedIn URN identifier |
| `page` | integer | Current page number |
| `count` | integer | Number of posts returned |
| `total` | integer | Total number of posts available |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/company/posts?url=https://www.linkedin.com/company/visualsoft-uk-ltd&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/company/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "url": "https://www.linkedin.com/company/visualsoft-uk-ltd",
        "page": 1
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "url": "https://www.linkedin.com/feed/update/urn:li:activity:7437505720176144385",
      "text": "Exciting news from our team...",
      "date": "2024-03-11 14:32:25",
      "author": "Visualsoft | Shopify Plus Partner",
      "author_description": "16,391 followers",
      "author_image": "https://media.licdn.com/...",
      "author_url": "https://www.linkedin.com/company/visualsoft-uk-ltd/posts",
      "likes": 13,
      "comments": 0,
      "shares": 5,
      "reactions": {
        "like": 10,
        "empathy": 3
      },
      "is_repost": false,
      "images": [],
      "video": {
        "thumbnail": "https://media.licdn.com/...",
        "duration": 102166
      },
      "links": ["https://www.linkedin.com/company/sportsshoes-com/"],
      "urn": "urn:li:activity:7437505720176144385"
    }
  ],
  "page": 1,
  "count": 10,
  "total": 462
}
```
