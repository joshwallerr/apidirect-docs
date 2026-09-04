# YouTube Video Comments

Get comments from any YouTube video by URL. Returns each comment's text, author, like count, reply count, publication date, a direct link, and up to 5 preview replies. Supports sorting by most recent or relevance, and fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/youtube/comments
```

**Price:** $0.005 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | YouTube video URL or 11-character video ID. Accepts `watch`, `youtu.be`, `shorts`, `embed`, and `live` URL forms. |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to ~100 comments. |
| `sort_by` | No | Sort order: `most_recent` (newest first) or `relevance` (default: `relevance`). |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `comments` | array | Array of comment threads (top-level comments) |
| `comments[].comment_id` | string | Unique comment ID |
| `comments[].text` | string | Comment text |
| `comments[].author` | string | Comment author's display name (handle) |
| `comments[].author_channel_id` | string | Comment author's channel ID |
| `comments[].author_channel_url` | string | Comment author's channel URL |
| `comments[].author_thumbnail` | string | Comment author's profile image URL |
| `comments[].likes` | integer | Number of likes on the comment |
| `comments[].reply_count` | integer | Total number of replies to the comment |
| `comments[].date` | string | Publication date and time |
| `comments[].updated_date` | string | Last edited date and time |
| `comments[].url` | string | Direct link to the comment |
| `comments[].video_id` | string | YouTube video ID |
| `comments[].channel_id` | string | Channel ID of the video |
| `comments[].source` | string | `"YouTube"` |
| `comments[].domain` | string | `"youtube.com"` |
| `comments[].replies` | array | Up to 5 preview replies. Each reply has `comment_id`, `text`, `author`, `author_channel_id`, `author_channel_url`, `author_thumbnail`, `likes`, `date`, `url`, `video_id`. |
| `pages` | integer | Number of pages requested (each page is billed) |
| `count` | integer | Total comments returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/youtube/comments?url=https://www.youtube.com/watch?v=dQw4w9WgXcQ&pages=1&sort_by=relevance" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/youtube/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "url": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
        "pages": 1,
        "sort_by": "relevance"
    }
)
print(response.json())
```

## Example Response

```json
{
  "comments": [
    {
      "comment_id": "Ugzge340dBgB75hWBm54AaABAg",
      "text": "can confirm: he never gave us up",
      "author": "@YouTube",
      "author_channel_id": "UCBR8-60-B28hp2BmDPdntcQ",
      "author_channel_url": "http://www.youtube.com/@YouTube",
      "author_thumbnail": "https://yt3.ggpht.com/.../photo.jpg",
      "likes": 261929,
      "reply_count": 1000,
      "date": "2025-04-22 19:05:08",
      "updated_date": "2025-04-22 19:05:08",
      "url": "https://youtube.com/watch?v=dQw4w9WgXcQ&lc=Ugzge340dBgB75hWBm54AaABAg",
      "video_id": "dQw4w9WgXcQ",
      "channel_id": "UCuAXFkgsw1L7xaCfnd5JJOw",
      "source": "YouTube",
      "domain": "youtube.com",
      "replies": [
        {
          "comment_id": "Ugzge340dBgB75hWBm54AaABAg.AHE8_QAWJx9AHE9eIiztxR",
          "text": "YOUTUBE AND ONE LIKE WOOHAAAAH",
          "author": "@linganguliguliwatcha",
          "author_channel_id": "UCjFRISlX-LPxiqViJAE3h6Q",
          "author_channel_url": "http://www.youtube.com/@linganguliguliwatcha",
          "author_thumbnail": "https://yt3.ggpht.com/.../photo.jpg",
          "likes": 7026,
          "date": "2025-04-22 19:14:32",
          "url": "https://youtube.com/watch?v=dQw4w9WgXcQ&lc=Ugzge340dBgB75hWBm54AaABAg.AHE8_QAWJx9AHE9eIiztxR",
          "video_id": "dQw4w9WgXcQ"
        }
      ]
    }
  ],
  "pages": 1,
  "count": 100
}
```

## Notes

- A video's pinned comment may appear first regardless of `sort_by`.
- Each page returns up to ~100 comments. Billing is per page requested.
- `replies` contains up to 5 preview replies per comment; a comment's full reply count is in `reply_count`.
- Videos with comments disabled (or otherwise unavailable) return an empty `comments` array.
- A nonexistent, private, or removed video returns `404` with code `video_not_found`.
