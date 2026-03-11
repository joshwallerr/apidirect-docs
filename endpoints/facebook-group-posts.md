# Facebook Group Posts

Get posts from a public Facebook group. Returns post content, author details, engagement metrics, and media. Only public groups can be scraped.

## Endpoint

```
GET /v1/facebook/group/posts
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `group_id` | Yes | Facebook group numeric ID |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |
| `sort_by` | No | Sort order: `most_recent` or `relevance` (default: `most_recent`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of group posts |
| `posts[].post_id` | string | Unique post identifier |
| `posts[].url` | string | Direct link to the post |
| `posts[].message` | string | Post text content |
| `posts[].date` | string | Publication date and time |
| `posts[].timestamp` | integer | Unix timestamp of publication |
| `posts[].author_name` | string | Name of the post author |
| `posts[].author_id` | string | Unique identifier of the author |
| `posts[].author_url` | string | Link to the author's profile |
| `posts[].author_profile_picture` | string | URL of the author's profile picture |
| `posts[].comments_count` | integer | Number of comments |
| `posts[].reactions_count` | integer | Total number of reactions |
| `posts[].reshare_count` | integer | Number of reshares |
| `posts[].reactions` | object | Breakdown of reaction types and counts |
| `posts[].image_url` | string/null | URL of attached image, if any |
| `posts[].video` | string/null | URL to attached video, if any |
| `posts[].external_url` | string/null | External link shared in the post, if any |
| `count` | integer | Number of posts returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/group/posts?group_id=1439220986320043&sort_by=most_recent" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/group/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "group_id": "1439220986320043",
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
      "post_id": "1439220986320043_8274610293847261",
      "url": "https://www.facebook.com/groups/1439220986320043/posts/8274610293847261",
      "message": "Just discovered a great new Python library for data visualization. Has anyone else tried Plotly Express? The syntax is so much cleaner than matplotlib.",
      "date": "2025-03-08 16:42:00",
      "timestamp": 1741452120,
      "author_name": "Sarah Chen",
      "author_id": "100042839174625",
      "author_url": "https://www.facebook.com/profile.php?id=100042839174625",
      "author_profile_picture": "https://scontent.fxxx.fbcdn.net/v/t1.6435-1/profile_pic.jpg",
      "comments_count": 23,
      "reactions_count": 87,
      "reshare_count": 12,
      "reactions": {
        "like": 54,
        "love": 18,
        "wow": 8,
        "haha": 3,
        "sad": 0,
        "angry": 0,
        "care": 4
      },
      "image_url": "https://scontent.fxxx.fbcdn.net/v/t39.30808-6/post_image.jpg",
      "video": null,
      "external_url": "https://plotly.com/python/plotly-express/"
    }
  ],
  "count": 20,
  "pages": 1
}
```
