# Bluesky Post Details

Get a single Bluesky post by URL or ID. Returns the post text, author, publication date, engagement metrics (likes, replies, reposts, quotes, bookmarks), media, link card, and quoted post.

## Endpoint

```
GET /v1/bluesky/post
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

Provide exactly one of `url` or `post_id`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Bluesky post URL, e.g. `https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l` (max 500 characters). Provide either `url` or `post_id`. |
| `post_id` | One required | The post's AT URI as returned in `post_id`, e.g. `at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l` (max 200 characters). Provide either `url` or `post_id`. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to the post. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `post` | object | Post data |
| `post.title` | string | Post title (format: `@handle on Bluesky`) |
| `post.url` | string | Direct link to the post |
| `post.date` | string | Publication date and time (UTC, YYYY-MM-DD HH:MM:SS) |
| `post.author` | string | Author's Bluesky handle |
| `post.author_name` | string | Author's display name |
| `post.author_id` | string | Author's DID (permanent account ID) |
| `post.author_verified` | boolean | Whether the author is verified |
| `post.source` | string | `"Bluesky"` |
| `post.domain` | string | `"bsky.app"` |
| `post.snippet` | string | Post text |
| `post.likes` | integer | Number of likes |
| `post.replies` | integer | Number of replies |
| `post.reposts` | integer | Number of reposts |
| `post.quotes` | integer | Number of quote posts |
| `post.bookmarks` | integer | Number of bookmarks |
| `post.lang` | string | Post language code (e.g. `en`), empty when not set |
| `post.is_reply` | boolean | Whether the post is a reply |
| `post.in_reply_to_id` | string | `post_id` of the post replied to (empty when not a reply) |
| `post.is_quote` | boolean | Whether the post quotes another post |
| `post.quoted_post` | object/null | The quoted post (`post_id`, `url`, `date`, `author`, `author_name`, `author_verified`, `snippet`, `likes`, `reposts`), or null |
| `post.hashtags` | string[] | Hashtags used in the post |
| `post.mentions` | string[] | Handles mentioned in the post |
| `post.links` | string[] | URLs linked in the post text |
| `post.link_preview` | object/null | Link card for posts sharing a URL (`url`, `title`, `description`, `image_url`), or null |
| `post.media_type` | string | `text`, `image`, `video`, or `carousel` |
| `post.image_url` | string | Full-size image URL for image posts, the thumbnail for video posts, empty for text-only |
| `post.video_url` | string | Video playlist URL (HLS) for video posts, empty otherwise |
| `post.carousel_media` | array | Images of a multi-image post (`image_url`, `thumbnail_url`, `alt`, `width`, `height`); empty otherwise |
| `post.post_id` | string | The post's AT URI (pass it as `post_id` to the post endpoints) |
| `post.sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `post.sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `post.sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `post.sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `post.sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/post?url=https%3A%2F%2Fbsky.app%2Fprofile%2Fbsky.app%2Fpost%2F3l6oveex3ii2l" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/post",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l"}
)
print(response.json())
```

## Example Response

```json
{
  "post": {
    "title": "@bsky.app on Bluesky",
    "url": "https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l",
    "date": "2024-10-17 07:06:51",
    "author": "bsky.app",
    "author_name": "Bluesky",
    "author_id": "did:plc:z72i7hdynmk6r22z27h6tvur",
    "author_verified": false,
    "source": "Bluesky",
    "domain": "bsky.app",
    "snippet": "👋  Bluesky is an open social network that gives creators independence from platforms, developers the freedom to build, and users a choice in their exp…",
    "likes": 63685,
    "replies": 8582,
    "reposts": 9530,
    "quotes": 708,
    "bookmarks": 249,
    "lang": "en",
    "is_reply": false,
    "in_reply_to_id": "",
    "is_quote": false,
    "quoted_post": null,
    "hashtags": [],
    "mentions": [],
    "links": [],
    "link_preview": null,
    "media_type": "text",
    "image_url": "",
    "video_url": "",
    "carousel_media": [],
    "post_id": "at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l"
  }
}
```
