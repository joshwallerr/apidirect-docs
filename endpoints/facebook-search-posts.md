# Facebook Search Posts

Search public Facebook posts by keyword. Returns post content, author details, engagement metrics, and media attachments.

## Endpoint

```
GET /v1/facebook/posts
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |
| `start_date` | No | Filter posts from this date onward (format: `YYYY-MM-DD`) |
| `end_date` | No | Filter posts up to this date (format: `YYYY-MM-DD`) |
| `sort_by` | No | Sort order: `most_recent` or `relevance` (default: `relevance`) |

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
curl "https://apidirect.io/v1/facebook/posts?query=artificial%20intelligence" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "artificial intelligence"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "post_id": "pfbid02kWx7vN9mJqR4hLcT3bY",
      "url": "https://www.facebook.com/permalink.php?story_fbid=pfbid02kWx7vN9mJqR4hLcT3bY&id=100064837291045",
      "message": "Artificial intelligence is transforming the way we approach medical diagnostics. A new study shows AI models can now detect early-stage cancers with 94% accuracy, outperforming traditional screening methods.",
      "date": "2025-03-09 11:20:00",
      "timestamp": 1741519200,
      "author_name": "TechNews Daily",
      "author_id": "100064837291045",
      "author_url": "https://www.facebook.com/TechNewsDaily",
      "author_profile_picture": "https://scontent.fxxx.fbcdn.net/v/t1.6435-1/profile_pic.jpg",
      "comments_count": 156,
      "reactions_count": 842,
      "reshare_count": 203,
      "reactions": {
        "like": 512,
        "love": 187,
        "wow": 98,
        "haha": 5,
        "sad": 12,
        "angry": 3,
        "care": 25
      },
      "image_url": "https://scontent.fxxx.fbcdn.net/v/t39.30808-6/ai_diagnostics.jpg",
      "video": null,
      "external_url": "https://technewsdaily.com/ai-cancer-detection-study"
    }
  ],
  "count": 20,
  "pages": 1
}
```
