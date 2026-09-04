# Instagram User Posts

Get a user's recent posts and reels (their feed) by profile URL or username. Returns post captions, engagement metrics (likes, comments, shares, views), author metadata, hashtags, and mentions. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/instagram/user/posts
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | No | Instagram profile URL, e.g. `https://instagram.com/natgeo` (max 500 characters). Provide either `url` or `username`. |
| `username` | No | Instagram username, with or without leading `@` (max 100 characters). Provide either `url` or `username`. |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to 12 posts. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

Provide exactly one of `url` or `username`.

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of the user's recent posts and reels |
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
| `posts[].media_type` | string | Post type (e.g., `"feed"`, `"clips"`, `"carousel_container"`) |
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
| `posts[].is_pinned` | boolean | Whether the post is pinned to the top of the user's profile |
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
curl "https://apidirect.io/v1/instagram/user/posts?url=https://instagram.com/natgeo&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/user/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "url": "https://instagram.com/natgeo",
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
      "title": "@natgeo on Instagram",
      "url": "https://instagram.com/p/DZkn1f0Flsc",
      "date": "2026-06-14 16:00:06",
      "author": "natgeo",
      "source": "Instagram",
      "domain": "instagram.com",
      "snippet": "Photograph by @petelas | A curious fox in the snow...",
      "likes": 530176,
      "comments": 5608,
      "shares": 9536,
      "reposts": 4353,
      "views": null,
      "is_video": false,
      "media_type": "carousel_container",
      "author_verified": true,
      "author_name": "National Geographic",
      "hashtags": [],
      "mentions": ["petelas"],
      "media_id": "3520497851234567890",
      "thumbnail_url": "https://scontent.cdninstagram.com/v/t51.82787-15/cover.jpg",
      "video_url": "",
      "video_duration": null,
      "width": 1080,
      "height": 1350,
      "carousel_media_count": 3,
      "is_paid_partnership": false,
      "location": {
        "name": "Serengeti National Park",
        "city": "Arusha",
        "lat": -2.3333,
        "lng": 34.8333
      },
      "tagged_users": [
        {"username": "natgeotv", "full_name": "National Geographic TV", "user_id": "18091046"}
      ],
      "coauthors": [],
      "carousel_media": [
        {"media_id": "3520497851234567891", "is_video": false, "image_url": "https://scontent.cdninstagram.com/v/t51.82787-15/slide1.jpg", "video_url": "", "width": 1080, "height": 1350},
        {"media_id": "3520497851234567892", "is_video": false, "image_url": "https://scontent.cdninstagram.com/v/t51.82787-15/slide2.jpg", "video_url": "", "width": 1080, "height": 1350},
        {"media_id": "3520497851234567893", "is_video": true, "image_url": "https://scontent.cdninstagram.com/v/t51.82787-15/slide3.jpg", "video_url": "https://scontent.cdninstagram.com/o1/v/t2/slide3.mp4", "width": 1080, "height": 1920}
      ],
      "audio": null,
      "is_pinned": false
    }
  ],
  "pages": 2,
  "count": 24
}
```

## Notes

- Posts are returned newest first, up to 12 per page. Use `pages` (1-20) to fetch more in a single call; you are billed per page requested.
- Both regular posts and Reels are returned. Use `media_type` to distinguish them (`clips` for Reels).
- If the account does not exist, the endpoint returns `404` with code `not_found`. You are not charged for `not_found` responses.
- Private accounts return no posts.
