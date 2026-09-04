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
| `pages` | No | Number of pages to fetch, 1-20 (default: 1) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

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
| `posts[].media_id` | string | Instagram media ID |
| `posts[].thumbnail_url` | string | URL of the post's cover image (temporary; valid ~6–24 hours) |
| `posts[].video_url` | string | Direct video URL for video posts/reels; empty for images (temporary; valid ~6–24 hours) |
| `posts[].video_duration` | number/null | Video length in seconds (`null` for images) |
| `posts[].width` | integer | Media width in pixels |
| `posts[].height` | integer | Media height in pixels |
| `posts[].carousel_media_count` | integer | Number of items in a carousel post (`0` for single-media posts) |
| `posts[].is_paid_partnership` | boolean | Whether the post is a paid partnership / branded content |
| `posts[].location` | object/null | Geotag: `name`, `city`, `lat`, `lng` (or `null`) |
| `posts[].tagged_users` | array | Users tagged in the post (`username`, `full_name`, `user_id`) |
| `posts[].coauthors` | array | Collaborators on the post (`username`, `full_name`, `user_id`, `is_verified`) |
| `posts[].carousel_media` | array | For carousel/album posts: each slide as `media_id`, `is_video`, `image_url`, `video_url`, `width`, `height` (empty for single-media posts) |
| `posts[].audio` | object/null | Audio track for reels/videos: `type` (`music` or `original`), `title`, `artist`, `audio_id`, `duration_ms` (`null` when no audio) |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
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
      "mentions": ["saudi_airlines"],
      "media_id": "3512345678901234567",
      "thumbnail_url": "https://scontent.cdninstagram.com/v/t51.82787-15/cover.jpg",
      "video_url": "https://scontent.cdninstagram.com/o1/v/t2/clip.mp4",
      "video_duration": 41.2,
      "width": 1080,
      "height": 1920,
      "carousel_media_count": 0,
      "is_paid_partnership": false,
      "location": null,
      "tagged_users": [
        {"username": "saudi_airlines", "full_name": "Saudia", "user_id": "12345678"}
      ],
      "coauthors": [],
      "carousel_media": [],
      "audio": {
        "type": "original",
        "title": "Original audio",
        "artist": "mrbeast",
        "audio_id": "1234567890123456",
        "duration_ms": 41200
      },
      "sentiment": {
        "emotions": {
          "joy": 40,
          "trust": 55,
          "fear": 0,
          "surprise": 10,
          "sadness": 0,
          "disgust": 0,
          "anger": 0,
          "anticipation": 30
        },
        "dominant_emotion": "trust",
        "emotional_intensity": 5,
        "polarity": "positive"
      }
    }
  ],
  "pages": 2,
  "count": 20
}
```
