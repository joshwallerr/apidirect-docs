# Threads User Posts

Get a user's recent posts (their feed) on Threads by username. Returns post text, engagement metrics (likes, replies, reposts, quotes, reshares), author metadata, attached media, link previews, and whether each post is pinned to the profile.

## Endpoint

```
GET /v1/threads/user/posts
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | Yes | Threads username, with or without leading @ (max 100 characters) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of the user's recent posts |
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
| `posts[].author_name` | string | Author's display name |
| `posts[].author_verified` | boolean | Whether the author is verified |
| `posts[].is_reply` | boolean | Whether the post is a reply |
| `posts[].is_pinned` | boolean | Whether the post is pinned to the top of the user's profile |
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
curl "https://apidirect.io/v1/threads/user/posts?username=mrbeast" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/threads/user/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "mrbeast"}
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "@mrbeast on Threads",
      "url": "https://www.threads.com/@mrbeast/post/DPb1G6SEocH",
      "date": "2025-10-05 16:49:10",
      "author": "mrbeast",
      "source": "Threads",
      "domain": "threads.com",
      "snippet": "When AI videos are just as good as normal videos, I wonder what that will do to the millions of creators making content for a living.",
      "likes": 9742,
      "replies": 1825,
      "reposts": 297,
      "quotes": 40,
      "reshares": 105,
      "author_name": "MrBeast",
      "author_verified": true,
      "is_reply": false,
      "is_pinned": false,
      "media_type": "text",
      "image_url": "",
      "video_url": "",
      "width": 0,
      "height": 0,
      "has_audio": false,
      "reply_control": "everyone",
      "hashtags": [],
      "mentions": [],
      "carousel_media": [],
      "link_preview": null,
      "quoted_post": null,
      "post_id": "3736813887196137223",
      "code": "DPb1G6SEocH"
    }
  ],
  "count": 25
}
```

## Notes

- Each request returns a single page of the user's most recent posts, newest first.