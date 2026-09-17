# Bluesky Post Quotes

Get the posts that quote a Bluesky post, newest first. Returns the full quoting post with its text, author, engagement metrics, and media.

## Endpoint

```
GET /v1/bluesky/post/quotes
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

Provide exactly one of `url` or `post_id`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Bluesky post URL, e.g. `https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l` (max 500 characters). Provide either `url` or `post_id`. |
| `post_id` | One required | The post's AT URI as returned in `post_id`, e.g. `at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l` (max 200 characters). Provide either `url` or `post_id`. |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to 50 posts; you are billed per page returned. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `quotes` | array | Array of quoting posts, newest first |
| `quotes[].title` | string | Post title (format: `@handle on Bluesky`) |
| `quotes[].url` | string | Direct link to the post |
| `quotes[].date` | string | Publication date and time (UTC, YYYY-MM-DD HH:MM:SS) |
| `quotes[].author` | string | Author's Bluesky handle |
| `quotes[].author_name` | string | Author's display name |
| `quotes[].author_id` | string | Author's DID (permanent account ID) |
| `quotes[].author_verified` | boolean | Whether the author is verified |
| `quotes[].source` | string | `"Bluesky"` |
| `quotes[].domain` | string | `"bsky.app"` |
| `quotes[].snippet` | string | Post text |
| `quotes[].likes` | integer | Number of likes |
| `quotes[].replies` | integer | Number of replies |
| `quotes[].reposts` | integer | Number of reposts |
| `quotes[].quotes` | integer | Number of quote posts |
| `quotes[].bookmarks` | integer | Number of bookmarks |
| `quotes[].lang` | string | Post language code (e.g. `en`), empty when not set |
| `quotes[].is_reply` | boolean | Whether the post is a reply |
| `quotes[].in_reply_to_id` | string | `post_id` of the post replied to (empty when not a reply) |
| `quotes[].is_quote` | boolean | Whether the post quotes another post |
| `quotes[].quoted_post` | object/null | The quoted post (`post_id`, `url`, `date`, `author`, `author_name`, `author_verified`, `snippet`, `likes`, `reposts`), or null |
| `quotes[].hashtags` | string[] | Hashtags used in the post |
| `quotes[].mentions` | string[] | Handles mentioned in the post |
| `quotes[].links` | string[] | URLs linked in the post text |
| `quotes[].link_preview` | object/null | Link card for posts sharing a URL (`url`, `title`, `description`, `image_url`), or null |
| `quotes[].media_type` | string | `text`, `image`, `video`, or `carousel` |
| `quotes[].image_url` | string | Full-size image URL for image posts, the thumbnail for video posts, empty for text-only |
| `quotes[].video_url` | string | Video playlist URL (HLS) for video posts, empty otherwise |
| `quotes[].carousel_media` | array | Images of a multi-image post (`image_url`, `thumbnail_url`, `alt`, `width`, `height`); empty otherwise |
| `quotes[].post_id` | string | The post's AT URI (pass it as `post_id` to the post endpoints) |
| `quotes[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `quotes[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `quotes[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `quotes[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `quotes[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `post_id` | string | The post's AT URI |
| `total` | integer | The post's total quote count |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/post/quotes?url=https%3A%2F%2Fbsky.app%2Fprofile%2Fbsky.app%2Fpost%2F3l6oveex3ii2l&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/post/quotes",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "quotes": [
    {
      "title": "@ekimdafluffyeevee.bsky.social on Bluesky",
      "url": "https://bsky.app/profile/ekimdafluffyeevee.bsky.social/post/3musg7o2nfk24",
      "date": "2026-09-05 21:26:54",
      "author": "ekimdafluffyeevee.bsky.social",
      "author_name": "michael_Mikafran",
      "author_id": "did:plc:aske3ha7qi4gm2fskxuxo64h",
      "author_verified": false,
      "source": "Bluesky",
      "domain": "bsky.app",
      "snippet": "open social network my ass being eaten by cannabis",
      "likes": 4,
      "replies": 0,
      "reposts": 0,
      "quotes": 0,
      "bookmarks": 0,
      "lang": "en",
      "is_reply": false,
      "in_reply_to_id": "",
      "is_quote": true,
      "quoted_post": {
        "post_id": "at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l",
        "url": "https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l",
        "date": "2024-10-17 07:06:51",
        "author": "bsky.app",
        "author_name": "Bluesky",
        "author_verified": false,
        "snippet": "👋  Bluesky is an open social network that gives creators independence from platforms, developers the freedom to build, a…",
        "likes": 63685,
        "reposts": 9530
      },
      "hashtags": [],
      "mentions": [],
      "links": [],
      "link_preview": null,
      "media_type": "text",
      "image_url": "",
      "video_url": "",
      "carousel_media": [],
      "post_id": "at://did:plc:aske3ha7qi4gm2fskxuxo64h/app.bsky.feed.post/3musg7o2nfk24"
    }
  ],
  "post_id": "at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l",
  "total": 708,
  "pages": 1,
  "count": 50
}
```
