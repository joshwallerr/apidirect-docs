# Facebook Page Posts

Get posts from a Facebook page by page ID. Returns post content, engagement metrics, reactions breakdown, and media. Supports fetching multiple pages in a single call and optional date filtering.

## Endpoint

```
GET /v1/facebook/page/posts
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `page_id` | Yes | Facebook page ID (get from page details or page ID endpoint) |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |
| `start_date` | No | Filter posts from this date (YYYY-MM-DD) |
| `end_date` | No | Filter posts up to this date (YYYY-MM-DD) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | List of post objects |
| `posts[].post_id` | string | Unique post ID |
| `posts[].url` | string | URL to the post |
| `posts[].message` | string | Post text content |
| `posts[].date` | string | Human-readable date |
| `posts[].timestamp` | integer | Unix timestamp |
| `posts[].author_name` | string | Name of the post author |
| `posts[].author_id` | string | Author's Facebook ID |
| `posts[].author_url` | string | URL to author's profile |
| `posts[].author_profile_picture` | string | URL to author's profile picture |
| `posts[].comments_count` | integer | Number of comments |
| `posts[].reactions_count` | integer | Total number of reactions |
| `posts[].reshare_count` | integer | Number of shares |
| `posts[].reactions` | object | Breakdown of reactions by type |
| `posts[].reactions.angry` | integer | Number of angry reactions |
| `posts[].reactions.care` | integer | Number of care reactions |
| `posts[].reactions.haha` | integer | Number of haha reactions |
| `posts[].reactions.like` | integer | Number of like reactions |
| `posts[].reactions.love` | integer | Number of love reactions |
| `posts[].reactions.sad` | integer | Number of sad reactions |
| `posts[].reactions.wow` | integer | Number of wow reactions |
| `posts[].image_url` | string/null | URL to attached image, if any |
| `posts[].video` | string/null | URL to attached video, if any |
| `posts[].external_url` | string/null | External link shared in the post, if any |
| `count` | integer | Number of posts returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/page/posts?page_id=100064860875397" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/page/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"page_id": "100064860875397"}
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "post_id": "890147362481953",
      "url": "https://www.facebook.com/facebook/posts/890147362481953",
      "message": "Introducing new ways to connect with the people and communities you care about most.",
      "date": "2025-12-14 18:30:00",
      "timestamp": 1734198600,
      "author_name": "Facebook",
      "author_id": "100064860875397",
      "author_url": "https://www.facebook.com/facebook",
      "author_profile_picture": "https://scontent.xx.fbcdn.net/v/t39.30808-1/277546_..._n.png",
      "comments_count": 1243,
      "reactions_count": 18742,
      "reshare_count": 3021,
      "reactions": {
        "angry": 84,
        "care": 210,
        "haha": 156,
        "like": 12847,
        "love": 4930,
        "sad": 23,
        "wow": 492
      },
      "image_url": "https://scontent.xx.fbcdn.net/v/t39.30808-6/472918_..._n.jpg",
      "video": null,
      "external_url": null
    }
  ],
  "count": 1,
  "pages": 1
}
```
