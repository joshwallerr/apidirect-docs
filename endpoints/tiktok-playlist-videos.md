# TikTok Playlist Videos

Get a playlist's videos in playlist order by playlist URL or numeric playlist ID. Returns the same fields as User Videos for each video, 30 per page.

## Endpoint

```
GET /v1/tiktok/playlist/videos
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `url` or `playlist_id`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | TikTok playlist URL, e.g. `https://www.tiktok.com/@natgeo/playlist/Cinematic-7509464647364283178` (max 500 characters). |
| `playlist_id` | One required | Numeric playlist ID: the number at the end of a playlist URL. |
| `pages` | No | Number of pages to fetch, 1-1000 (default: 1). Each page returns up to 30 videos. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `videos` | array | Array of the playlist's videos in playlist order |
| `videos[].video_id` | string | Numeric video ID |
| `videos[].title` | string | Video caption |
| `videos[].url` | string | Direct link to the video |
| `videos[].date` | string | Publication date and time |
| `videos[].date_timestamp` | integer/null | Publication date as a Unix timestamp |
| `videos[].author` | string | Author's TikTok username |
| `videos[].source` | string | `"TikTok"` |
| `videos[].domain` | string | `"tiktok.com"` |
| `videos[].snippet` | string | Video caption text |
| `videos[].region` | string | 2-letter region code the video was posted from |
| `videos[].play_count` | integer | Number of plays/views |
| `videos[].likes` | integer | Number of likes |
| `videos[].comments` | integer | Number of comments |
| `videos[].shares` | integer | Number of shares |
| `videos[].downloads` | integer | Number of downloads |
| `videos[].saves` | integer | Number of saves (favorites) |
| `videos[].duration` | integer | Video duration in seconds (0 for photo posts) |
| `videos[].is_ad` | boolean | Whether the video is an ad |
| `videos[].is_pinned` | boolean | Whether the video is pinned to the author's profile |
| `videos[].author_name` | string | Author's display name |
| `videos[].author_id` | string | Author's numeric user ID |
| `videos[].author_avatar` | string | Author's avatar URL |
| `videos[].author_url` | string | Link to the author's profile |
| `videos[].cover` | string | Video cover/thumbnail URL |
| `videos[].dynamic_cover` | string | Animated cover URL |
| `videos[].origin_cover` | string | Original cover frame URL |
| `videos[].video_url` | string | Watermark-free playback/download URL (temporary) |
| `videos[].video_url_watermarked` | string | Watermarked playback URL (temporary) |
| `videos[].size` | integer | File size of the watermark-free video in bytes |
| `videos[].size_watermarked` | integer | File size of the watermarked video in bytes |
| `videos[].images` | string[] | Image URLs for photo posts; empty for videos |
| `videos[].music_url` | string | Playback URL of the sound |
| `videos[].mentioned_user_ids` | string[] | Numeric IDs of the users mentioned in the caption |
| `videos[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `videos[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `videos[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `videos[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `videos[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `playlist_id` | string | The playlist's numeric ID |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/playlist/videos?url=https://www.tiktok.com/@natgeo/playlist/Cinematic-7509464647364283178" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/playlist/videos",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.tiktok.com/@natgeo/playlist/Cinematic-7509464647364283178"}
)
print(response.json())
```

## Example Response

```json
{
  "videos": [
    {
      "video_id": "7509066418168597791",
      "title": "Spring in Patagonia is a time of abundance, and this puma mother has cubs to feed",
      "url": "https://www.tiktok.com/@natgeo/video/7509066418168597791",
      "date": "2025-05-27 10:14:17",
      "date_timestamp": 1748340857,
      "author": "natgeo",
      "source": "TikTok",
      "domain": "tiktok.com",
      "snippet": "Spring in Patagonia is a time of abundance, and this puma mother has cubs to feed",
      "region": "GB",
      "play_count": 31112,
      "likes": 1268,
      "comments": 31,
      "shares": 44,
      "downloads": 1,
      "saves": 51,
      "duration": 20,
      "is_ad": false,
      "is_pinned": false,
      "author_name": "National Geographic",
      "author_id": "6780344874811442181",
      "author_avatar": "https://p16-common-sign.tiktokcdn-eu.com/.../avatar.jpeg",
      "author_url": "https://www.tiktok.com/@natgeo",
      "cover": "https://p16-common-sign.tiktokcdn-eu.com/.../cover.jpeg",
      "dynamic_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../dynamic_cover.webp",
      "origin_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../origin_cover.jpeg",
      "video_url": "https://v19.tiktokcdn-eu.com/.../video.mp4",
      "video_url_watermarked": "https://v19.tiktokcdn-eu.com/.../video_wm.mp4",
      "size": 3008834,
      "size_watermarked": 0,
      "images": [],
      "music_url": "https://sf16-music.tiktokcdn-eu.com/.../music.mp3",
      "mentioned_user_ids": [
        "6763618106315375621"
      ]
    }
  ],
  "playlist_id": "7509464647364283178",
  "pages": 1,
  "count": 27
}
```
