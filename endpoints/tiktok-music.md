# TikTok Music Details

Get a sound's details by music URL or numeric music ID. Returns its title, artist, album, duration, playback URL, cover image, and the number of videos using it.

## Endpoint

```
GET /v1/tiktok/music
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `url` or `music_id`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | TikTok music URL, e.g. `https://www.tiktok.com/music/Face-Off-7016547803243022337` (max 500 characters). |
| `music_id` | One required | Numeric music ID: the number at the end of a music URL, also returned as music_id on every video. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `music` | object | Sound data |
| `music.music_id` | string | Numeric music ID |
| `music.title` | string | Sound title |
| `music.artist` | string | Artist / creator of the sound |
| `music.album` | string | Album, or empty string |
| `music.is_original` | boolean | Whether it is an original sound rather than a licensed track |
| `music.duration` | integer | Duration in seconds |
| `music.play_url` | string | Audio playback URL |
| `music.cover` | string | Cover image URL |
| `music.video_count` | integer | Number of videos using the sound |
| `music.url` | string | Link to the sound page |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/music?url=https://www.tiktok.com/music/Face-Off-7016547803243022337" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/music",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.tiktok.com/music/Face-Off-7016547803243022337"}
)
print(response.json())
```

## Example Response

```json
{
  "music": {
    "music_id": "7016547803243022337",
    "title": "Face Off - Dwayne Johnson",
    "artist": "Tech N9ne & Joey Cool & King Iso & Dwayne Johnson",
    "album": "Face Off - Dwayne Johnson",
    "is_original": false,
    "duration": 60,
    "play_url": "https://sf16-ies-music-sg.tiktokcdn.com/.../audio.mp3",
    "cover": "https://p16-sg.tiktokcdn.com/.../cover.jpeg",
    "video_count": 729613,
    "url": "https://www.tiktok.com/music/Face-Off-Dwayne-Johnson-7016547803243022337"
  }
}
```
