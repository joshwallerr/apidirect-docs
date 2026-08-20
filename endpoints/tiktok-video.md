# TikTok Video Details

Get full details for a single TikTok video by URL or video ID. Returns the caption, play / like / comment / share / save counts, watermark-free playback and download URLs, cover images, music track info, and author details.

## Endpoint

```
GET /v1/tiktok/video
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `url` or `video_id`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | TikTok video URL, e.g. `https://www.tiktok.com/@tiktok/video/7516594811734854943` (max 500 characters) |
| `video_id` | One required | Numeric TikTok video ID, as returned by [Search Videos](/docs/tiktok-videos) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `video` | object | Video data |
| `video.video_id` | string | TikTok video ID |
| `video.url` | string | Link to the video |
| `video.title` | string | Video caption |
| `video.region` | string | 2-letter region code the video was posted from |
| `video.date` | string | Date and time the video was published |
| `video.date_timestamp` | integer/null | Unix timestamp of the publish date |
| `video.duration` | integer | Video length in seconds |
| `video.play_count` | integer | Number of plays |
| `video.likes` | integer | Number of likes |
| `video.comments` | integer | Number of comments |
| `video.shares` | integer | Number of shares |
| `video.downloads` | integer | Number of downloads |
| `video.saves` | integer | Number of times the video was saved / favorited |
| `video.is_ad` | boolean | Whether the video is a paid ad |
| `video.cover` | string | URL to the video cover image |
| `video.dynamic_cover` | string | URL to the animated cover image |
| `video.origin_cover` | string | URL to the original still cover frame |
| `video.video_url` | string | Watermark-free MP4 URL (temporary signed link) |
| `video.video_url_hd` | string | Original-quality MP4 URL (temporary signed link), or empty string |
| `video.video_url_watermarked` | string | Watermarked MP4 URL (temporary signed link) |
| `video.size` | integer | File size of the watermark-free MP4 in bytes |
| `video.size_hd` | integer | File size of the original-quality MP4 in bytes |
| `video.size_watermarked` | integer | File size of the watermarked MP4 in bytes |
| `video.author` | string | Author's TikTok username |
| `video.author_name` | string | Author's display name |
| `video.author_id` | string | Author's TikTok user ID |
| `video.author_avatar` | string | URL to the author's profile picture |
| `video.author_url` | string | Link to the author's profile |
| `video.music_id` | string | TikTok ID of the music track |
| `video.music_title` | string | Music track title |
| `video.music_author` | string | Music track artist / creator |
| `video.music_url` | string | MP3 URL for the music track (temporary signed link) |
| `video.music_cover` | string | URL to the music track's cover image |
| `video.music_album` | string | Album name, or empty string |
| `video.music_original` | boolean | Whether the track is an original sound |
| `video.music_duration` | integer | Music track length in seconds |
| `video.mentioned_user_ids` | array | User IDs of accounts mentioned in the caption |

If the video does not exist, the endpoint returns a `404` with `code: "not_found"`.

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/video?url=https://www.tiktok.com/@tiktok/video/7516594811734854943" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/video",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.tiktok.com/@tiktok/video/7516594811734854943"}
)
print(response.json())
```

You can also pass a numeric video ID instead of a URL:

```bash
curl "https://apidirect.io/v1/tiktok/video?video_id=7516594811734854943" \
  -H "X-API-Key: YOUR_API_KEY"
```

## Example Response

```json
{
  "video": {
    "video_id": "7516594811734854943",
    "url": "https://www.tiktok.com/@tiktok/video/7516594811734854943",
    "title": "🌈🐬🦄 life after @Zara Larsson Symphony vocals 🌈🐬🦄",
    "region": "US",
    "date": "2025-06-16 17:07:10",
    "date_timestamp": 1750093630,
    "duration": 66,
    "play_count": 18912653,
    "likes": 879920,
    "comments": 4382,
    "shares": 17420,
    "downloads": 1003,
    "saves": 38685,
    "is_ad": true,
    "cover": "https://p16-common-sign.tiktokcdn-us.com/.../cover.jpeg",
    "dynamic_cover": "https://p16-common-sign.tiktokcdn-us.com/.../dynamic.image",
    "origin_cover": "https://p16-common-sign.tiktokcdn-us.com/.../origin.webp",
    "video_url": "https://v16m.tiktokcdn-us.com/.../video.mp4",
    "video_url_hd": "https://v16.tokcdn.com/.../7516594811734854943_original.mp4",
    "video_url_watermarked": "https://v16m.tiktokcdn-us.com/.../video_wm.mp4",
    "size": 7786703,
    "size_hd": 38711004,
    "size_watermarked": 7988034,
    "author": "tiktok",
    "author_name": "TikTok",
    "author_id": "107955",
    "author_avatar": "https://p19-common-sign.tiktokcdn-us.com/.../avatar.jpeg",
    "author_url": "https://www.tiktok.com/@tiktok",
    "music_id": "7516599978421209887",
    "music_title": "original sound - tiktok",
    "music_author": "TikTok",
    "music_url": "https://v16-ies-music.tiktokcdn-us.com/.../audio.mp3",
    "music_cover": "https://p16-common-sign.tiktokcdn-us.com/.../music.jpeg",
    "music_album": "",
    "music_original": true,
    "music_duration": 66,
    "mentioned_user_ids": ["205879097384816641"]
  }
}
```

## Notes

- `video_url`, `video_url_hd`, `video_url_watermarked`, and `music_url` are temporary signed CDN links that expire after a few hours. Request the video again whenever you need fresh links.
- `video_url_hd` is the original upload quality and is usually a much larger file (see `size_hd`).
