# Bluesky Posts

Search Bluesky posts by keyword. Returns post text, author, publication date, engagement metrics (likes, replies, reposts, quotes, bookmarks), media, link cards, and quoted posts. Supports sorting, a date window, and fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/bluesky/posts
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters). Bluesky search syntax works: `"exact phrase"`, `-exclude`, `from:handle`, `lang:en`, `#tag` |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to 50 posts; you are billed per page returned. |
| `sort_by` | No | Sort order: `most_recent` or `relevance` (default: `most_recent`) |
| `start_date` | No | Only posts from this date onward (format: `YYYY-MM-DD`) |
| `end_date` | No | Only posts up to this date (format: `YYYY-MM-DD`) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching posts |
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
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/posts?query=anthropic&pages=1&sort_by=most_recent" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "anthropic", "pages": 1, "sort_by": "most_recent"}
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "@papoo7.bsky.social on Bluesky",
      "url": "https://bsky.app/profile/papoo7.bsky.social/post/3mvnldg3l2u24",
      "date": "2026-09-16 16:40:21",
      "author": "papoo7.bsky.social",
      "author_name": "",
      "author_id": "did:plc:57j4dnzyvdjl2bici4u3oero",
      "author_verified": false,
      "source": "Bluesky",
      "domain": "bsky.app",
      "snippet": "Anthropic is asking for brakes after helping build the car\nhttps://papoo.work/doc/f150d1ed17a55c33\n#claudenews #anthropic #claude #llm #agents",
      "likes": 0,
      "replies": 0,
      "reposts": 0,
      "quotes": 0,
      "bookmarks": 0,
      "lang": "en",
      "is_reply": false,
      "in_reply_to_id": "",
      "is_quote": false,
      "quoted_post": null,
      "hashtags": [
        "claudenews",
        "anthropic",
        "claude",
        "llm",
        "agents"
      ],
      "mentions": [],
      "links": [
        "https://papoo.work/doc/f150d1ed17a55c33"
      ],
      "link_preview": {
        "url": "https://papoo.work/doc/f150d1ed17a55c33",
        "title": "Anthropic is asking for brakes after helping build the car",
        "description": "",
        "image_url": "https://cdn.bsky.app/img/feed_thumbnail/plain/did:plc:57j4dnzyvdjl2bici4u3oero/bafkreib5cpnglprvtxzloallnma2vwnzypd2t2nr…"
      },
      "media_type": "text",
      "image_url": "",
      "video_url": "",
      "carousel_media": [],
      "post_id": "at://did:plc:57j4dnzyvdjl2bici4u3oero/app.bsky.feed.post/3mvnldg3l2u24"
    }
  ],
  "pages": 1,
  "count": 50
}
```

## Notes

- Each page returns up to 50 posts; you are billed per page returned, so a search that runs out of results early is billed only for what came back.
