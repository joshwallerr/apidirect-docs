# Facebook Group Search

Search posts within a specific Facebook group by keyword. Returns matching posts with content, author details, and engagement metrics.

## Endpoint

```
GET /v1/facebook/group/search
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `group_id` | Yes | Facebook group numeric ID |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |
| `start_date` | No | Filter posts from this date onward (format: `YYYY-MM-DD`) |
| `end_date` | No | Filter posts up to this date (format: `YYYY-MM-DD`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching posts |
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
curl "https://apidirect.io/v1/facebook/group/search?query=help&group_id=137206643664121" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/group/search",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "help",
        "group_id": "137206643664121"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "post_id": "137206643664121_5920384710283746",
      "url": "https://www.facebook.com/groups/137206643664121/posts/5920384710283746",
      "message": "Can anyone help me debug this React component? I keep getting a hydration mismatch error when using useEffect with server-side rendering.",
      "date": "2025-03-07 09:15:00",
      "timestamp": 1741338900,
      "author_name": "James Rivera",
      "author_id": "100058271640392",
      "author_url": "https://www.facebook.com/profile.php?id=100058271640392",
      "author_profile_picture": "https://scontent.fxxx.fbcdn.net/v/t1.6435-1/profile_pic.jpg",
      "comments_count": 41,
      "reactions_count": 15,
      "reshare_count": 2,
      "reactions": {
        "like": 10,
        "love": 1,
        "wow": 0,
        "haha": 0,
        "sad": 2,
        "angry": 0,
        "care": 2
      },
      "image_url": null,
      "video": null,
      "external_url": null
    }
  ],
  "count": 15,
  "pages": 1
}
```
