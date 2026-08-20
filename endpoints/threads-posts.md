# Threads Posts

Search Threads posts by keyword. Returns post text, engagement metrics (likes, replies, reposts, quotes, reshares), author metadata, attached media, and link previews.

## Endpoint

```
GET /v1/threads/posts
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching posts |
| `posts[].title` | string | Post title (format: @username on Threads) |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time (UTC, YYYY-MM-DD HH:MM:SS) |
| `posts[].author` | string | Author's Threads username |
| `posts[].source` | string | `"Threads"` |
| `posts[].domain` | string | `"threads.com"` |
| `posts[].snippet` | string | Post text content |
| `posts[].likes` | integer | Number of likes |
| `posts[].replies` | integer | Number of replies |
| `posts[].reposts` | integer | Number of reposts |
| `posts[].quotes` | integer | Number of quote posts |
| `posts[].reshares` | integer | Number of times reshared to other surfaces |
| `posts[].author_name` | string | Author's display name (empty on some search results) |
| `posts[].author_verified` | boolean | Whether the author is verified |
| `posts[].is_reply` | boolean | Whether the post is a reply |
| `posts[].media_type` | string | Post type: `text`, `image`, `video`, or `carousel` |
| `posts[].image_url` | string | Cover image URL for image/video/carousel posts, empty for text-only (temporary; valid ~6-24 hours) |
| `posts[].video_url` | string | Direct video URL for video posts, empty otherwise (temporary; valid ~6-24 hours) |
| `posts[].width` | integer | Media width in pixels (0 when not applicable) |
| `posts[].height` | integer | Media height in pixels (0 when not applicable) |
| `posts[].has_audio` | boolean | Whether the post's video has audio |
| `posts[].reply_control` | string | Who can reply (e.g. `everyone`) |
| `posts[].hashtags` | array | Hashtags used in the post |
| `posts[].mentions` | array | Usernames mentioned in the post |
| `posts[].carousel_media` | array | Slides for carousel posts (`media_id`, `is_video`, `image_url`, `video_url`, `width`, `height`); empty otherwise |
| `posts[].link_preview` | object \| null | Link preview for posts sharing a URL (`url`, `display_url`, `title`, `description`, `image_url`, `favicon_url`), or null |
| `posts[].quoted_post` | object \| null | The embedded quoted/reposted post (same post shape), or null |
| `posts[].post_id` | string | Threads post ID |
| `posts[].code` | string | Post shortcode (used in the post URL) |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/threads/posts?query=technology" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/threads/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "technology"}
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "@technologybrief on Threads",
      "url": "https://www.threads.com/@technologybrief/post/DaqCqtWHdiU",
      "date": "2026-07-08 14:22:31",
      "author": "technologybrief",
      "source": "Threads",
      "domain": "threads.com",
      "snippet": "Most people don't realize how many tech giants are already deep in bear-market territory.",
      "likes": 1284,
      "replies": 96,
      "reposts": 41,
      "quotes": 12,
      "reshares": 23,
      "author_name": "Technology Brief",
      "author_verified": true,
      "is_reply": false,
      "media_type": "image",
      "image_url": "https://scontent.cdninstagram.com/v/t51.82787-15/photo.jpg",
      "video_url": "",
      "width": 1080,
      "height": 1350,
      "has_audio": false,
      "reply_control": "everyone",
      "hashtags": [],
      "mentions": [],
      "carousel_media": [],
      "link_preview": null,
      "quoted_post": null,
      "post_id": "3938972555089402004",
      "code": "DaqCqtWHdiU"
    }
  ],
  "count": 25
}
```