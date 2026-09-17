# Bluesky User Likes

Get the posts a Bluesky user has liked, newest first. Returns the full post for each like plus `liked_at`, the time the user liked it.

## Endpoint

```
GET /v1/bluesky/user/likes
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
| `posts` | array | Array of liked posts, most recently liked first |
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
| `posts[].liked_at` | string | When the user liked the post |
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
curl "https://apidirect.io/v1/bluesky/user/likes?username=pfrazee.com&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/user/likes",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "pfrazee.com", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "@cthomasjamh.bsky.social on Bluesky",
      "url": "https://bsky.app/profile/cthomasjamh.bsky.social/post/3mvnh4tvkfc2j",
      "date": "2026-09-16 15:25:06",
      "author": "cthomasjamh.bsky.social",
      "author_name": "Charlie Thomas",
      "author_id": "did:plc:he2lkvdpuq3vnsnludc2r5im",
      "author_verified": false,
      "source": "Bluesky",
      "domain": "bsky.app",
      "snippet": "I am actually going to start trying to use Sankey diagrams in every briefing I do from now on while watching the reactions of the audience like a hawk…",
      "likes": 22,
      "replies": 1,
      "reposts": 4,
      "quotes": 1,
      "bookmarks": 0,
      "lang": "en",
      "is_reply": false,
      "in_reply_to_id": "",
      "is_quote": true,
      "quoted_post": {
        "post_id": "at://did:plc:ragtjsm2j2vknwkz3zp4oxrd/app.bsky.feed.post/3mvm4gtzkgk2f",
        "url": "https://bsky.app/profile/pfrazee.com/post/3mvm4gtzkgk2f",
        "date": "2026-09-16 02:41:11",
        "author": "pfrazee.com",
        "author_name": "P(aul) Frazee",
        "author_verified": true,
        "snippet": "I’m gonna need a moratorium on sankey diagrams",
        "likes": 311,
        "reposts": 17
      },
      "hashtags": [],
      "mentions": [],
      "links": [],
      "link_preview": null,
      "media_type": "text",
      "image_url": "",
      "video_url": "",
      "carousel_media": [],
      "post_id": "at://did:plc:he2lkvdpuq3vnsnludc2r5im/app.bsky.feed.post/3mvnh4tvkfc2j",
      "liked_at": "2026-09-16 16:43:04"
    }
  ],
  "username": "pfrazee.com",
  "pages": 1,
  "count": 50
}
```
