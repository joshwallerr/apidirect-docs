# YouTube Video Details

Get detailed information about a YouTube video by URL or video ID. Returns title, full description, channel name and ID, publish date, duration, view count, category, keywords, and thumbnail.

## Endpoint

```
GET /v1/youtube/video
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | YouTube video URL (`watch?v=`, `youtu.be/`, `/shorts/`, `/embed/` or `/live/` forms) or 11-character video ID |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `video` | object | Video data |
| `video.video_id` | string | YouTube video ID |
| `video.url` | string | Link to the video |
| `video.title` | string | Video title |
| `video.description` | string | Full video description |
| `video.author` | string | Channel name |
| `video.channel_id` | string | YouTube channel ID |
| `video.date` | string | Date and time the video was published (UTC) |
| `video.duration` | integer/null | Video length in seconds |
| `video.views` | integer/null | Number of views |
| `video.category` | string | YouTube category (e.g. `Music`) |
| `video.type` | string | Video type as reported by YouTube (e.g. `NORMAL`) |
| `video.is_live` | boolean | Whether the video is a live stream |
| `video.keywords` | array | The video's tags |
| `video.thumbnail` | string | URL to the highest resolution thumbnail |

If the video does not exist, the endpoint returns a `404` with `code: "video_not_found"`.

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/youtube/video?url=https://www.youtube.com/watch?v=dQw4w9WgXcQ" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/youtube/video",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.youtube.com/watch?v=dQw4w9WgXcQ"}
)
print(response.json())
```

You can also pass an 11-character video ID instead of a URL:

```bash
curl "https://apidirect.io/v1/youtube/video?url=dQw4w9WgXcQ" \
  -H "X-API-Key: YOUR_API_KEY"
```

## Example Response

```json
{
  "video": {
    "video_id": "dQw4w9WgXcQ",
    "url": "https://youtube.com/watch?v=dQw4w9WgXcQ",
    "title": "Rick Astley - Never Gonna Give You Up (Official Video) (4K Remaster)",
    "description": "The official video for “Never Gonna Give You Up” by Rick Astley...",
    "author": "Rick Astley",
    "channel_id": "UCuAXFkgsw1L7xaCfnd5JJOw",
    "date": "2009-10-25 06:57:33",
    "duration": 213,
    "views": 1788679598,
    "category": "Music",
    "type": "NORMAL",
    "is_live": false,
    "keywords": ["rick astley", "Never Gonna Give You Up", "rick roll"],
    "thumbnail": "https://i.ytimg.com/vi_webp/dQw4w9WgXcQ/maxresdefault.webp"
  }
}
```

## Notes

- Works for regular videos, Shorts, and live streams alike.
- For live streams, `is_live` is `true` and `duration` reflects the elapsed stream time so far.
