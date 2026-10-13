# TikTok Hashtag Videos

Get the videos under a hashtag by name, numeric hashtag ID, or hashtag URL. Returns the same fields as User Videos for each video, about 20 per page.

## Endpoint

```
GET /v1/tiktok/hashtag/videos
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `name`, `hashtag_id`, or `url`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `name` | One required | Hashtag name, with or without leading `#` (max 100 characters). |
| `hashtag_id` | One required | Numeric hashtag ID, as returned by [Search Hashtags](/docs/tiktok-hashtags). |
| `url` | One required | TikTok hashtag URL, e.g. `https://www.tiktok.com/tag/cooking` (max 500 characters). |
| `pages` | No | Number of pages to fetch, 1-1000 (default: 1). Each page returns up to 20 videos. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `videos` | array | Array of videos under the hashtag |
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
| `hashtag` | string | The hashtag name (empty when looked up by hashtag_id) |
| `hashtag_id` | string | The hashtag's numeric ID |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/hashtag/videos?name=cooking&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/hashtag/videos",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "name": "cooking",
        "pages": 2
    }
)
print(response.json())
```

## Example Response

```json
{
  "videos": [
    {
      "video_id": "7692609313717636383",
      "title": "#recipes #EasyRecipe #cooking #DinnerIdeas",
      "url": "https://www.tiktok.com/@cooking_recipescr/video/7692609313717636383",
      "date": "2026-10-04 00:49:32",
      "date_timestamp": 1791074972,
      "author": "cooking_recipescr",
      "source": "TikTok",
      "domain": "tiktok.com",
      "snippet": "#recipes #EasyRecipe #cooking #DinnerIdeas",
      "region": "US",
      "play_count": 431691,
      "likes": 5002,
      "comments": 108,
      "shares": 1638,
      "downloads": 449,
      "saves": 3558,
      "duration": 1435,
      "is_ad": false,
      "is_pinned": false,
      "author_name": "cooking_recipescr",
      "author_id": "7352666564073833515",
      "author_avatar": "https://p16-common-sign.tiktokcdn-eu.com/.../avatar.jpeg",
      "author_url": "https://www.tiktok.com/@cooking_recipescr",
      "cover": "https://p16-common-sign.tiktokcdn-eu.com/.../cover.jpeg",
      "dynamic_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../dynamic_cover.webp",
      "origin_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../origin_cover.jpeg",
      "video_url": "https://v19.tiktokcdn-eu.com/.../video.mp4",
      "video_url_watermarked": "https://v19.tiktokcdn-eu.com/.../video_wm.mp4",
      "size": 10246341,
      "size_watermarked": 9402354,
      "images": [],
      "music_id": "7692609536951110431",
      "music_title": "original sound - cooking_recipescr",
      "music_author": "cooking_recipescr",
      "music_url": "https://sf16-music.tiktokcdn-eu.com/.../music.mp3",
      "music_cover": "https://p16-common-sign.tiktokcdn-eu.com/.../music_cover.jpeg",
      "music_album": "",
      "music_original": true,
      "music_duration": 1420,
      "mentioned_user_ids": []
    }
  ],
  "hashtag": "cooking",
  "hashtag_id": "18973",
  "pages": 2,
  "count": 40
}
```
