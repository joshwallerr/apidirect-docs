# Instagram Hashtag Posts

Get posts and reels for an Instagram hashtag. Returns captions, engagement metrics, author metadata, media URLs, and the hashtag's total post count. Supports the top, recent, and reels tabs, and pagination.

## Endpoint

```
GET /v1/instagram/hashtag/posts
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `hashtag` | Yes | Hashtag, with or without the leading `#` (max 100 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1). Each page adds up to about 30 posts; repeats across pages are removed. |
| `sort_by` | No | Hashtag tab: `top`, `recent`, or `reels` (default: `top`) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of posts and reels for the hashtag |
| `posts[].title` | string | Post title (format: `@username on Instagram`) |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Instagram username |
| `posts[].source` | string | `"Instagram"` |
| `posts[].domain` | string | `"instagram.com"` |
| `posts[].snippet` | string | Post caption text |
| `posts[].likes` | integer/null | Number of likes (`null` when the author hides like counts) |
| `posts[].comments` | integer | Number of comments |
| `posts[].shares` | integer | Number of shares |
| `posts[].reposts` | integer | Number of reposts |
| `posts[].views` | integer/null | Number of views/plays (`null` for image posts) |
| `posts[].is_video` | boolean | Whether the post is a video |
| `posts[].media_type` | string | Post type (e.g., `feed`, `clips`, `carousel_container`) |
| `posts[].author_verified` | boolean | Whether the author is verified |
| `posts[].author_name` | string | Author's display name |
| `posts[].hashtags` | string[] | Hashtags used in the caption |
| `posts[].mentions` | string[] | Usernames mentioned in the caption |
| `posts[].media_id` | string | Instagram media ID |
| `posts[].thumbnail_url` | string | URL of the post's cover image (temporary; valid ~6-24 hours) |
| `posts[].video_url` | string | Direct video URL for video posts/reels; empty for images (temporary; valid ~6-24 hours) |
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
| `hashtag` | string | The requested hashtag, without `#` |
| `total` | integer/null | Total number of posts using the hashtag (`null` for `recent`) |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/hashtag/posts?hashtag=summer&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/hashtag/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "hashtag": "summer",
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
      "title": "@chloeaustenn19 on Instagram",
      "url": "https://instagram.com/p/DcvNO0YDqxz",
      "date": "2026-09-01 08:14:01",
      "author": "chloeaustenn19",
      "source": "Instagram",
      "domain": "instagram.com",
      "snippet": "am i cute? #chicago #style #summer",
      "likes": 6009,
      "comments": 107,
      "shares": 228,
      "reposts": 0,
      "views": 372196,
      "is_video": true,
      "media_type": "clips",
      "author_verified": false,
      "author_name": "Chloe",
      "hashtags": [
        "#chicago",
        "#style",
        "#summer"
      ],
      "mentions": [],
      "media_id": "3976455188906945651",
      "thumbnail_url": "https://scontent.cdninstagram.com/v/t51.71878-15/cover.jpg",
      "video_url": "https://scontent.cdninstagram.com/o1/v/t2/clip.mp4",
      "video_duration": 10.1,
      "width": 1080,
      "height": 1920,
      "carousel_media_count": 0,
      "is_paid_partnership": false,
      "location": null,
      "tagged_users": [],
      "coauthors": [],
      "carousel_media": [],
      "audio": {
        "type": "original",
        "title": "Original audio",
        "artist": "chloeaustenn19",
        "audio_id": "38320043790943785",
        "duration_ms": 10076
      }
    }
  ],
  "hashtag": "summer",
  "total": 578259801,
  "pages": 2,
  "count": 64
}
```

## Notes

- Each page adds up to about 30 posts (repeats across pages are removed); you are billed per page requested.
