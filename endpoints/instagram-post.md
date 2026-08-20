# Instagram Post Details

Get full details for a single Instagram post, reel, or IGTV video by URL or shortcode. Returns the caption, like / comment / share / view counts, media URLs, carousel slides, audio track info, tagged users, location, and author details.

## Endpoint

```
GET /v1/instagram/post
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `url` or `code`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Instagram post, reel, or story URL, e.g. `https://www.instagram.com/p/CxYQJO8xuC6/` (max 500 characters). `/p/`, `/reel/`, `/tv/`, and `/stories/` URLs are accepted. |
| `code` | One required | The post's shortcode from the URL, e.g. `CxYQJO8xuC6`, or its numeric media ID (max 50 characters) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to the post. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `post` | object | Post data |
| `post.title` | string | Post title (format: `@username on Instagram`) |
| `post.url` | string | Direct link to the post |
| `post.date` | string | Publication date and time |
| `post.date_timestamp` | integer/null | Unix timestamp of the publication date |
| `post.author` | string | Instagram username |
| `post.author_id` | string | Author's Instagram user ID |
| `post.source` | string | Platform name (Instagram) |
| `post.domain` | string | instagram.com |
| `post.snippet` | string | Post caption text |
| `post.likes` | integer | Number of likes |
| `post.comments` | integer | Number of comments |
| `post.shares` | integer | Number of shares |
| `post.reposts` | integer | Number of reposts |
| `post.views` | integer/null | Number of views/plays (null for image posts) |
| `post.is_video` | boolean | Whether the post is a video |
| `post.media_type` | string | Post type: `feed`, `clips` (reel), or `carousel_container` |
| `post.author_verified` | boolean | Whether the author is verified |
| `post.author_name` | string | Author's display name |
| `post.hashtags` | array | Hashtags used in the caption |
| `post.mentions` | array | Usernames mentioned in the caption |
| `post.media_id` | string | Instagram media ID |
| `post.thumbnail_url` | string | URL of the post's cover image (temporary; valid ~6-24 hours) |
| `post.video_url` | string | Direct video URL for video posts/reels, empty for images (temporary; valid ~6-24 hours) |
| `post.video_duration` | number/null | Video length in seconds (null for images) |
| `post.width` | integer | Media width in pixels |
| `post.height` | integer | Media height in pixels |
| `post.carousel_media_count` | integer | Number of items in a carousel post (0 for single-media posts) |
| `post.is_paid_partnership` | boolean | Whether the post is a paid partnership / branded content |
| `post.location` | object/null | Geotag with `name`, `city`, `lat`, `lng` (null when the post has no location) |
| `post.tagged_users` | array | Users tagged in the post (`username`, `full_name`, `user_id`) |
| `post.coauthors` | array | Collaborators on the post (`username`, `full_name`, `user_id`, `is_verified`) |
| `post.carousel_media` | array | For carousel/album posts: one entry per slide with `media_id`, `is_video`, `image_url`, `video_url`, `width`, `height` (empty for single-media posts) |
| `post.audio` | object/null | Audio track for reels/videos: `type` (`music` or `original`), `title`, `artist`, `audio_id`, `duration_ms` (null when the post has no audio) |
| `post.is_pinned` | boolean | Whether the post is pinned to the top of the author's profile |
| `post.accessibility_caption` | string | Auto-generated alt text describing the image (empty when unavailable) |
| `post.sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `post.sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `post.sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `post.sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `post.sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |

If the post does not exist, the endpoint returns a `404` with `code: "not_found"`.

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/post?url=https://www.instagram.com/reel/DaTSSukB-Lb/" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/post",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.instagram.com/reel/DaTSSukB-Lb/"}
)
print(response.json())
```

You can also pass the post's shortcode instead of a URL:

```bash
curl "https://apidirect.io/v1/instagram/post?code=DaTSSukB-Lb" \
  -H "X-API-Key: YOUR_API_KEY"
```

## Example Response

```json
{
  "post": {
    "title": "@instagram on Instagram",
    "url": "https://instagram.com/p/DaTSSukB-Lb",
    "date": "2026-07-02 18:58:11",
    "date_timestamp": 1783018691,
    "author": "instagram",
    "author_id": "25025320",
    "source": "Instagram",
    "domain": "instagram.com",
    "snippet": "this glow >>> #InTheMoment Video by @chriswoodlight Music by Amory Reel",
    "likes": 167541,
    "comments": 2493,
    "shares": 13063,
    "reposts": 0,
    "views": 21786137,
    "is_video": true,
    "media_type": "clips",
    "author_verified": true,
    "author_name": "Instagram",
    "hashtags": ["#InTheMoment"],
    "mentions": ["chriswoodlight"],
    "media_id": "3932567351408976603",
    "thumbnail_url": "https://scontent.cdninstagram.com/v/t51.82787-15/cover.jpg",
    "video_url": "https://scontent.cdninstagram.com/o1/v/t2/video.mp4",
    "video_duration": 22.03,
    "width": 720,
    "height": 1280,
    "carousel_media_count": 0,
    "is_paid_partnership": false,
    "location": null,
    "tagged_users": [
      {"username": "chriswoodlight", "full_name": "Chris Wood Light Studio", "user_id": "2107151539"}
    ],
    "coauthors": [],
    "carousel_media": [],
    "audio": {
      "type": "music",
      "title": "her garden",
      "artist": "Amory Reel",
      "audio_id": "7115801341882925",
      "duration_ms": 89205
    },
    "is_pinned": false,
    "accessibility_caption": ""
  }
}
```

## Notes

- `thumbnail_url`, `video_url`, and carousel media URLs are temporary CDN links that expire after roughly 6-24 hours. Request the post again whenever you need fresh links.
- Reels return `media_type` `clips` plus `views`, `video_url`, `video_duration`, and the `audio` track. Carousel posts return `media_type` `carousel_container` and one `carousel_media` entry per slide.
