# Instagram User Stories

Get a user's active stories by username or profile URL. Returns each story's media URLs, post time and expiry, link stickers, mentions, tagged users, location, and audio.

## Endpoint

```
GET /v1/instagram/user/stories
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Instagram username, with or without leading `@` (max 100 characters). Provide either `username` or `url`. |
| `url` | One required | Instagram profile URL, e.g. `https://instagram.com/natgeo` (max 500 characters). Provide either `username` or `url`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `stories` | array | Array of the user's active stories, oldest first |
| `stories[].title` | string | Story title (format: `@username on Instagram`) |
| `stories[].url` | string | Direct link to the story |
| `stories[].date` | string | Publication date and time |
| `stories[].date_timestamp` | integer/null | Publication date as a Unix timestamp |
| `stories[].expires_at` | string | Expiry date and time |
| `stories[].expires_at_timestamp` | integer/null | Expiry as a Unix timestamp |
| `stories[].author` | string | Instagram username |
| `stories[].author_id` | string | Author's Instagram user ID |
| `stories[].author_name` | string | Author's display name |
| `stories[].author_verified` | boolean | Whether the author is verified |
| `stories[].source` | string | `"Instagram"` |
| `stories[].domain` | string | `"instagram.com"` |
| `stories[].snippet` | string | Story caption text (usually empty) |
| `stories[].is_video` | boolean | Whether the story is a video |
| `stories[].media_type` | string | `"story"` |
| `stories[].media_id` | string | Instagram media ID |
| `stories[].thumbnail_url` | string | Story image or video cover (temporary; valid ~6-24 hours) |
| `stories[].video_url` | string | Direct video URL for video stories, empty for images (temporary; valid ~6-24 hours) |
| `stories[].video_duration` | number/null | Video length in seconds (`null` for images) |
| `stories[].width` | integer | Media width in pixels |
| `stories[].height` | integer | Media height in pixels |
| `stories[].location` | object/null | Geotag: `name`, `city`, `lat`, `lng` (or `null`) |
| `stories[].tagged_users` | array | Users tagged in the story (`username`, `full_name`, `user_id`) |
| `stories[].mentions` | string[] | Usernames mentioned in the story |
| `stories[].links` | array | Link stickers (`url`, `title`) |
| `stories[].audio` | object/null | Audio track: `type`, `title`, `artist`, `audio_id`, `duration_ms` (`null` when none) |
| `stories[].coauthors` | array | Collaborators on the story (`username`, `full_name`, `user_id`, `is_verified`) |
| `stories[].is_paid_partnership` | boolean | Whether the story is a paid partnership |
| `username` | string | The requested username |
| `count` | integer | Number of stories returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/user/stories?username=natgeo" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/user/stories",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "username": "natgeo"
    }
)
print(response.json())
```

## Example Response

```json
{
  "stories": [
    {
      "title": "@natgeo on Instagram",
      "url": "https://instagram.com/stories/natgeo/3976510169036109894/",
      "date": "2026-09-01 10:02:53",
      "date_timestamp": 1788256973,
      "expires_at": "2026-09-02 10:02:53",
      "expires_at_timestamp": 1788343373,
      "author": "natgeo",
      "author_id": "787132",
      "author_name": "National Geographic",
      "author_verified": true,
      "source": "Instagram",
      "domain": "instagram.com",
      "snippet": "",
      "is_video": false,
      "media_type": "story",
      "media_id": "3976510169036109894",
      "thumbnail_url": "https://scontent.cdninstagram.com/v/t51.82787-15/story.jpg",
      "video_url": "",
      "video_duration": null,
      "width": 750,
      "height": 1334,
      "location": null,
      "tagged_users": [],
      "mentions": [],
      "links": [
        {
          "url": "https://www.nationalgeographic.com/environment/article/super-el-nino-extreme-weather-climate",
          "title": "Visit Link"
        }
      ],
      "audio": null,
      "coauthors": [],
      "is_paid_partnership": false
    }
  ],
  "username": "natgeo",
  "count": 3
}
```

## Notes

- Stories expire 24 hours after posting. An account with no active stories (or a private account) returns an empty `stories` array.
- `thumbnail_url` and `video_url` are temporary CDN links that expire after roughly 6-24 hours.
