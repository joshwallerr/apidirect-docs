# TikTok Playlist Details

Get a playlist's details by playlist URL or numeric playlist ID. Returns its name, creator, and video count.

## Endpoint

```
GET /v1/tiktok/playlist
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `url` or `playlist_id`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | TikTok playlist URL, e.g. `https://www.tiktok.com/@natgeo/playlist/Cinematic-7509464647364283178` (max 500 characters). |
| `playlist_id` | One required | Numeric playlist ID: the number at the end of a playlist URL. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `playlist` | object | Playlist data |
| `playlist.playlist_id` | string | Numeric playlist ID |
| `playlist.name` | string | Playlist name |
| `playlist.video_count` | integer | Number of videos in the playlist |
| `playlist.author` | string | Creator's TikTok username |
| `playlist.author_url` | string | Link to the creator's profile |
| `playlist.url` | string | Link to the playlist |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/playlist?url=https://www.tiktok.com/@natgeo/playlist/Cinematic-7509464647364283178" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/playlist",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.tiktok.com/@natgeo/playlist/Cinematic-7509464647364283178"}
)
print(response.json())
```

## Example Response

```json
{
  "playlist": {
    "playlist_id": "7509464647364283178",
    "name": "Cinematic",
    "video_count": 27,
    "author": "natgeo",
    "author_url": "https://www.tiktok.com/@natgeo",
    "url": "https://www.tiktok.com/@natgeo/playlist/Cinematic-7509464647364283178"
  }
}
```
