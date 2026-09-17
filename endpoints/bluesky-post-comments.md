# Bluesky Post Comments

Get the replies to a Bluesky post. Returns every reply Bluesky serves for the thread, nested up to 10 levels deep, as a flat list; each reply is a full post with `in_reply_to_id` pointing at its parent.

## Endpoint

```
GET /v1/bluesky/post/comments
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

Provide exactly one of `url` or `post_id`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Bluesky post URL, e.g. `https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l` (max 500 characters). Provide either `url` or `post_id`. |
| `post_id` | One required | The post's AT URI as returned in `post_id`, e.g. `at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l` (max 200 characters). Provide either `url` or `post_id`. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `comments` | array | Array of replies, thread order (a reply is followed by the replies to it) |
| `comments[].title` | string | Post title (format: `@handle on Bluesky`) |
| `comments[].url` | string | Direct link to the post |
| `comments[].date` | string | Publication date and time (UTC, YYYY-MM-DD HH:MM:SS) |
| `comments[].author` | string | Author's Bluesky handle |
| `comments[].author_name` | string | Author's display name |
| `comments[].author_id` | string | Author's DID (permanent account ID) |
| `comments[].author_verified` | boolean | Whether the author is verified |
| `comments[].source` | string | `"Bluesky"` |
| `comments[].domain` | string | `"bsky.app"` |
| `comments[].snippet` | string | Post text |
| `comments[].likes` | integer | Number of likes |
| `comments[].replies` | integer | Number of replies |
| `comments[].reposts` | integer | Number of reposts |
| `comments[].quotes` | integer | Number of quote posts |
| `comments[].bookmarks` | integer | Number of bookmarks |
| `comments[].lang` | string | Post language code (e.g. `en`), empty when not set |
| `comments[].is_reply` | boolean | Whether the post is a reply |
| `comments[].in_reply_to_id` | string | `post_id` of the post replied to (empty when not a reply) |
| `comments[].is_quote` | boolean | Whether the post quotes another post |
| `comments[].quoted_post` | object/null | The quoted post (`post_id`, `url`, `date`, `author`, `author_name`, `author_verified`, `snippet`, `likes`, `reposts`), or null |
| `comments[].hashtags` | string[] | Hashtags used in the post |
| `comments[].mentions` | string[] | Handles mentioned in the post |
| `comments[].links` | string[] | URLs linked in the post text |
| `comments[].link_preview` | object/null | Link card for posts sharing a URL (`url`, `title`, `description`, `image_url`), or null |
| `comments[].media_type` | string | `text`, `image`, `video`, or `carousel` |
| `comments[].image_url` | string | Full-size image URL for image posts, the thumbnail for video posts, empty for text-only |
| `comments[].video_url` | string | Video playlist URL (HLS) for video posts, empty otherwise |
| `comments[].carousel_media` | array | Images of a multi-image post (`image_url`, `thumbnail_url`, `alt`, `width`, `height`); empty otherwise |
| `comments[].post_id` | string | The post's AT URI (pass it as `post_id` to the post endpoints) |
| `comments[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `comments[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `comments[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `comments[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `comments[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `post_id` | string | The post's AT URI |
| `total` | integer | The post's total reply count |
| `count` | integer | Number of replies returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/post/comments?url=https%3A%2F%2Fbsky.app%2Fprofile%2Fbsky.app%2Fpost%2F3l6oveex3ii2l" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/post/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l"}
)
print(response.json())
```

## Example Response

```json
{
  "comments": [
    {
      "title": "@bsky.app on Bluesky",
      "url": "https://bsky.app/profile/bsky.app/post/3l6ovfftinx2m",
      "date": "2024-10-17 07:07:26",
      "author": "bsky.app",
      "author_name": "Bluesky",
      "author_id": "did:plc:z72i7hdynmk6r22z27h6tvur",
      "author_verified": false,
      "source": "Bluesky",
      "domain": "bsky.app",
      "snippet": "• Anyone can create and subscribe to feeds. There are 50k+ feeds here, like posts from mutuals, news, or cat photos!\n\nbsky.app/feeds\n\n• The Discover f…",
      "likes": 3254,
      "replies": 60,
      "reposts": 284,
      "quotes": 41,
      "bookmarks": 7,
      "lang": "en",
      "is_reply": true,
      "in_reply_to_id": "at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l",
      "is_quote": false,
      "quoted_post": null,
      "hashtags": [],
      "mentions": [],
      "links": [
        "https://bsky.app/feeds"
      ],
      "link_preview": null,
      "media_type": "text",
      "image_url": "",
      "video_url": "",
      "carousel_media": [],
      "post_id": "at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6ovfftinx2m"
    }
  ],
  "post_id": "at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l",
  "total": 8582,
  "count": 740
}
```

## Notes

- One request returns the whole thread Bluesky serves; there is no `pages` parameter. Very large threads come back as a bounded slice (a few hundred replies, nested at most 10 levels deep) with no way to page further, so `count` can be well below `total`, the post's full reply count.
