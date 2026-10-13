# TikTok User Stories

Get a user's currently live stories (the 24-hour posts shown on their profile) by username, numeric user ID, or profile URL. Returns the same fields as User Videos for each story. A user with no live stories returns an empty list.

## Endpoint

```
GET /v1/tiktok/user/stories
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `username`, `user_id`, or `url`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | TikTok username, with or without leading `@` (max 100 characters). |
| `user_id` | One required | Numeric TikTok user ID, as returned by [Search Users](/docs/tiktok-users) or [User Profile](/docs/tiktok-user). |
| `url` | One required | TikTok profile URL, e.g. `https://www.tiktok.com/@tiktok` (max 500 characters). |
| `pages` | No | Number of pages to fetch, 1-1000 (default: 1). Each page returns up to 30 stories. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `stories` | array | Array of the user's live stories |
| `stories[].video_id` | string | Numeric video ID |
| `stories[].title` | string | Video caption |
| `stories[].url` | string | Direct link to the video |
| `stories[].date` | string | Publication date and time |
| `stories[].date_timestamp` | integer/null | Publication date as a Unix timestamp |
| `stories[].author` | string | Author's TikTok username |
| `stories[].source` | string | `"TikTok"` |
| `stories[].domain` | string | `"tiktok.com"` |
| `stories[].snippet` | string | Video caption text |
| `stories[].region` | string | 2-letter region code the video was posted from |
| `stories[].play_count` | integer | Number of plays/views |
| `stories[].likes` | integer | Number of likes |
| `stories[].comments` | integer | Number of comments |
| `stories[].shares` | integer | Number of shares |
| `stories[].downloads` | integer | Number of downloads |
| `stories[].saves` | integer | Number of saves (favorites) |
| `stories[].duration` | integer | Video duration in seconds (0 for photo posts) |
| `stories[].is_ad` | boolean | Whether the video is an ad |
| `stories[].is_pinned` | boolean | Whether the video is pinned to the author's profile |
| `stories[].author_name` | string | Author's display name |
| `stories[].author_id` | string | Author's numeric user ID |
| `stories[].author_avatar` | string | Author's avatar URL |
| `stories[].author_url` | string | Link to the author's profile |
| `stories[].cover` | string | Video cover/thumbnail URL |
| `stories[].dynamic_cover` | string | Animated cover URL |
| `stories[].origin_cover` | string | Original cover frame URL |
| `stories[].video_url` | string | Watermark-free playback/download URL (temporary) |
| `stories[].video_url_watermarked` | string | Watermarked playback URL (temporary) |
| `stories[].size` | integer | File size of the watermark-free video in bytes |
| `stories[].size_watermarked` | integer | File size of the watermarked video in bytes |
| `stories[].images` | string[] | Image URLs for photo posts; empty for videos |
| `stories[].music_id` | string | ID of the sound used |
| `stories[].music_title` | string | Title of the sound used |
| `stories[].music_author` | string | Artist of the sound used |
| `stories[].music_url` | string | Playback URL of the sound |
| `stories[].music_cover` | string | Cover image of the sound |
| `stories[].music_album` | string | Album of the sound, or empty string |
| `stories[].music_original` | boolean | Whether the sound is an original sound |
| `stories[].music_duration` | integer | Sound duration in seconds |
| `stories[].mentioned_user_ids` | string[] | Numeric IDs of the users mentioned in the caption |
| `stories[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `stories[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `stories[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `stories[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `stories[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `username` | string | The user's username |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/user/stories?username=jamescharles" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/user/stories",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "jamescharles"}
)
print(response.json())
```

## Example Response

```json
{
  "stories": [
    {
      "video_id": "7695841671082216717",
      "title": "",
      "url": "https://www.tiktok.com/@jamescharles/video/7695841671082216717",
      "date": "2026-10-12 17:56:33",
      "date_timestamp": 1791827793,
      "author": "jamescharles",
      "source": "TikTok",
      "domain": "tiktok.com",
      "snippet": "",
      "region": "US",
      "play_count": 55471,
      "likes": 1352,
      "comments": 0,
      "shares": 25,
      "downloads": 0,
      "saves": 0,
      "duration": 7,
      "is_ad": false,
      "is_pinned": false,
      "author_name": "James Charles",
      "author_id": "190068318278651904",
      "author_avatar": "https://p16-common-sign.tiktokcdn-eu.com/.../avatar.jpeg",
      "author_url": "https://www.tiktok.com/@jamescharles",
      "cover": "https://p16-common-sign.tiktokcdn-eu.com/.../cover.jpeg",
      "dynamic_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../dynamic_cover.webp",
      "origin_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../origin_cover.jpeg",
      "video_url": "https://v19.tiktokcdn-eu.com/.../video.mp4",
      "video_url_watermarked": "https://v19.tiktokcdn-eu.com/.../video_wm.mp4",
      "size": 10246341,
      "size_watermarked": 9402354,
      "images": [],
      "music_id": "7695565970584193805",
      "music_title": "original sound - darth.amidalaa",
      "music_author": "darth amidala",
      "music_url": "https://sf16-music.tiktokcdn-eu.com/.../music.mp3",
      "music_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../music_cover.jpeg",
      "music_album": "",
      "music_original": true,
      "music_duration": 7,
      "mentioned_user_ids": []
    }
  ],
  "username": "jamescharles",
  "pages": 1,
  "count": 3
}
```
