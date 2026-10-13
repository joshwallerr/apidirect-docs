# TikTok User Likes

Get the videos a user has liked, by username, numeric user ID, or profile URL. Returns the same fields as User Videos for each liked video. Accounts that hide their liked videos return an empty list.

## Endpoint

```
GET /v1/tiktok/user/likes
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
| `pages` | No | Number of pages to fetch, 1-1000 (default: 1). Each page returns up to 30 videos. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `videos` | array | Array of videos the user has liked, most recent first |
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
| `videos[].music_id` | string | ID of the sound used |
| `videos[].music_title` | string | Title of the sound used |
| `videos[].music_author` | string | Artist of the sound used |
| `videos[].music_url` | string | Playback URL of the sound |
| `videos[].music_cover` | string | Cover image of the sound |
| `videos[].music_album` | string | Album of the sound, or empty string |
| `videos[].music_original` | boolean | Whether the sound is an original sound |
| `videos[].music_duration` | integer | Sound duration in seconds |
| `videos[].mentioned_user_ids` | string[] | Numeric IDs of the users mentioned in the caption |
| `videos[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `videos[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `videos[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `videos[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `videos[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `username` | string | The requested username (empty when looked up by user_id) |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/user/likes?username=bbcnews" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/user/likes",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "bbcnews"}
)
print(response.json())
```

## Example Response

```json
{
  "videos": [
    {
      "video_id": "7686739862707424534",
      "title": "Buckingham Palace strongly pushed back on Wednesday against claims made in a new book",
      "url": "https://www.tiktok.com/@bbcnews/video/7686739862707424534",
      "date": "2026-09-18 05:16:16",
      "date_timestamp": 1789708576,
      "author": "bbcnews",
      "source": "TikTok",
      "domain": "tiktok.com",
      "snippet": "Buckingham Palace strongly pushed back on Wednesday against claims made in a new book",
      "region": "GB",
      "play_count": 444580,
      "likes": 15934,
      "comments": 791,
      "shares": 487,
      "downloads": 90,
      "saves": 1007,
      "duration": 71,
      "is_ad": false,
      "is_pinned": false,
      "author_name": "BBC News",
      "author_id": "6953176899251241989",
      "author_avatar": "https://p16-common-sign.tiktokcdn-eu.com/.../avatar.jpeg",
      "author_url": "https://www.tiktok.com/@bbcnews",
      "cover": "https://p16-common-sign.tiktokcdn-eu.com/.../cover.jpeg",
      "dynamic_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../dynamic_cover.webp",
      "origin_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../origin_cover.jpeg",
      "video_url": "https://v19.tiktokcdn-eu.com/.../video.mp4",
      "video_url_watermarked": "https://v19.tiktokcdn-eu.com/.../video_wm.mp4",
      "size": 10246341,
      "size_watermarked": 9402354,
      "images": [],
      "music_id": "7686739934060890902",
      "music_title": "original sound - bbcnews",
      "music_author": "BBC News",
      "music_url": "https://sf16-music.tiktokcdn-eu.com/.../music.mp3",
      "music_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../music_cover.jpeg",
      "music_album": "",
      "music_original": true,
      "music_duration": 71,
      "mentioned_user_ids": []
    }
  ],
  "username": "bbcnews",
  "pages": 1,
  "count": 15
}
```
