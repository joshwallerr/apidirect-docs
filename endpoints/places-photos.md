# Place Photos

Get photos and videos for a place by `place_id`. Returns photo URLs (standard and high-resolution), capture coordinates, and timestamps.

## Endpoint

```
GET /v1/places/photos
```

**Price:** $0.01 per page
**Free tier:** 20 requests/month

Each page returns up to 10 photos.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `place_id` | Yes | Google `place_id`, as returned by the [Places Search](/docs/places-search) endpoint |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1). Each page returns up to 10 items and is billed as one request |
| `country` | No | 2-letter ISO 3166-1 alpha-2 region code (default: `us`) |
| `language` | No | 2-letter ISO 639-1 language code (default: `en`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `photos` | array | Array of photos and videos. Filter on the `type` field if you only want one |
| `photos[].photo_id` | string | Stable photo identifier |
| `photos[].type` | string | `photo` or `video` |
| `photos[].photo_url` | string | Standard-resolution image URL |
| `photos[].photo_url_large` | string \| null | High-resolution image URL (typically 3000–4000px wide). `null` for items where no large variant exists (some videos and older photos) |
| `photos[].video_thumbnail_url` | string \| null | Video thumbnail URL (set only when `type` is `video`) |
| `photos[].latitude` | number \| null | Capture latitude |
| `photos[].longitude` | number \| null | Capture longitude |
| `photos[].photo_datetime_utc` | string | ISO 8601 capture datetime (UTC) |
| `photos[].photo_timestamp` | integer | Unix timestamp (seconds) |
| `count` | integer | Total photos returned |
| `pages` | integer | Echo of requested pages |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/places/photos?place_id=ChIJifIePKtZwokRVZ-UdRGkZzs&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/places/photos",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "place_id": "ChIJifIePKtZwokRVZ-UdRGkZzs",
        "pages": 2,
    }
)
data = response.json()
print(f"Got {data['count']} photos across {data['pages']} pages")
```

## Example Response

```json
{
  "photos": [
    {
      "photo_id": "CIABIhAViB6GuQB0Czq6u1UIyD60",
      "type": "photo",
      "photo_url": "https://lh3.googleusercontent.com/gps-cs-s/APNQkAH...",
      "photo_url_large": "https://lh3.googleusercontent.com/gps-cs-s/APNQkAH...=w4280-h3407-k-no",
      "video_thumbnail_url": null,
      "latitude": 40.7546469,
      "longitude": -73.9868158,
      "photo_datetime_utc": "2026-05-30T00:00:00.000Z",
      "photo_timestamp": 1780099200
    },
    {
      "photo_id": "CIHM0ogKEICAgICGgNfJ4wE",
      "type": "video",
      "photo_url": "https://lh3.googleusercontent.com/gps-cs-s/...",
      "photo_url_large": null,
      "video_thumbnail_url": "https://lh3.googleusercontent.com/gps-cs-s/...=w640-h360-k-no",
      "latitude": 40.7546795,
      "longitude": -73.9870291,
      "photo_datetime_utc": "2021-11-16T00:00:00.000Z",
      "photo_timestamp": 1637020800
    }
  ],
  "count": 20,
  "pages": 2
}
```

## Notes

- `photo_url_large` is the full-resolution version of the photo. Some videos and older photos don't have a large variant — the field is `null` in that case.
- The `type` field is `"photo"` or `"video"`. Filter client-side if you only want one.
- Photos are typically returned newest-first based on upload date.
