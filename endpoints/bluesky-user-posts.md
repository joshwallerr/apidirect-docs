# Bluesky User Posts

Get a user's feed by handle: their posts, replies, and reposts in feed order (the pinned post first, then newest first), each flagged with `is_reply`, `is_repost`, and `is_pinned`. Returns post text, engagement metrics, media, link cards, and quoted posts.

## Endpoint

```
GET /v1/bluesky/user/posts
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

Provide exactly one of `username` or `url`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Bluesky handle, e.g. `bsky.app`, with or without leading `@`, or the account's DID (max 100 characters). Provide either `username` or `url`. |
| `url` | One required | Bluesky profile URL, e.g. `https://bsky.app/profile/bsky.app` (max 500 characters). Provide either `username` or `url`. |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to 50 posts; you are billed per page returned. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of the user's feed items: the pinned post first (if any), then newest first |
| `posts[].title` | string | Post title (format: `@handle on Bluesky`) |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time (UTC, YYYY-MM-DD HH:MM:SS) |
| `posts[].author` | string | Author's Bluesky handle |
| `posts[].author_name` | string | Author's display name |
| `posts[].author_id` | string | Author's DID (permanent account ID) |
| `posts[].author_verified` | boolean | Whether the author is verified |
| `posts[].source` | string | `"Bluesky"` |
| `posts[].domain` | string | `"bsky.app"` |
| `posts[].snippet` | string | Post text |
| `posts[].likes` | integer | Number of likes |
| `posts[].replies` | integer | Number of replies |
| `posts[].reposts` | integer | Number of reposts |
| `posts[].quotes` | integer | Number of quote posts |
| `posts[].bookmarks` | integer | Number of bookmarks |
| `posts[].lang` | string | Post language code (e.g. `en`), empty when not set |
| `posts[].is_reply` | boolean | Whether the post is a reply |
| `posts[].in_reply_to_id` | string | `post_id` of the post replied to (empty when not a reply) |
| `posts[].is_quote` | boolean | Whether the post quotes another post |
| `posts[].quoted_post` | object/null | The quoted post (`post_id`, `url`, `date`, `author`, `author_name`, `author_verified`, `snippet`, `likes`, `reposts`), or null |
| `posts[].hashtags` | string[] | Hashtags used in the post |
| `posts[].mentions` | string[] | Handles mentioned in the post |
| `posts[].links` | string[] | URLs linked in the post text |
| `posts[].link_preview` | object/null | Link card for posts sharing a URL (`url`, `title`, `description`, `image_url`), or null |
| `posts[].media_type` | string | `text`, `image`, `video`, or `carousel` |
| `posts[].image_url` | string | Full-size image URL for image posts, the thumbnail for video posts, empty for text-only |
| `posts[].video_url` | string | Video playlist URL (HLS) for video posts, empty otherwise |
| `posts[].carousel_media` | array | Images of a multi-image post (`image_url`, `thumbnail_url`, `alt`, `width`, `height`); empty otherwise |
| `posts[].post_id` | string | The post's AT URI (pass it as `post_id` to the post endpoints) |
| `posts[].is_repost` | boolean | Whether this item is a repost by the user (the post fields describe the original post) |
| `posts[].reposted_by` | string | Handle of the user who reposted it (empty when not a repost) |
| `posts[].is_pinned` | boolean | Whether the post is pinned to the user's profile |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `username` | string | The requested handle or DID |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/user/posts?username=bsky.app&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/user/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "bsky.app", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
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
      "post_id": "at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l",
      "is_repost": false,
      "reposted_by": "",
      "is_pinned": true
    }
  ],
  "username": "bsky.app",
  "pages": 1,
  "count": 50
}
```
