# Instagram Highlight Stories

Get the stories saved in a highlight by highlight ID or URL. Returns the highlight's title and cover, plus each story's media URLs, post date, link stickers, mentions, tagged users, location, and audio.

## Endpoint

```
GET /v1/instagram/highlight/stories
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `highlight_id` | Yes | Highlight ID from the User Highlights endpoint, e.g. `17987606483520330`, or a highlight URL like `https://www.instagram.com/stories/highlights/17987606483520330/` (max 500 characters) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `highlight` | object | The highlight |
| `highlight.highlight_id` | string | Highlight ID |
| `highlight.title` | string | Highlight title |
| `highlight.media_count` | integer | Number of stories in the highlight |
| `highlight.cover_url` | string | Cover image URL (temporary; valid ~6-24 hours) |
| `highlight.created_at` | string | Creation date and time |
| `highlight.created_at_timestamp` | integer/null | Creation date as a Unix timestamp |
| `highlight.updated_at` | string | Date and time a story was last added |
| `highlight.updated_at_timestamp` | integer/null | Last-updated date as a Unix timestamp |
| `highlight.is_pinned` | boolean | Whether the highlight is pinned on the profile |
| `highlight.url` | string | Direct link to the highlight |
| `highlight.author` | string | Owner's Instagram username |
| `highlight.author_id` | string | Owner's Instagram user ID |
| `stories` | array | The stories in the highlight, oldest first |
| `stories[].title` | string | Story title (format: `@username on Instagram`) |
| `stories[].url` | string | Direct link to the story |
| `stories[].date` | string | Publication date and time |
| `stories[].date_timestamp` | integer/null | Publication date as a Unix timestamp |
| `stories[].expires_at` | string | Always empty (highlight stories do not expire) |
| `stories[].expires_at_timestamp` | integer/null | Always `null` (highlight stories do not expire) |
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
| `count` | integer | Number of stories returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/highlight/stories?highlight_id=17987606483520330" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/highlight/stories",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "highlight_id": "17987606483520330"
    }
)
print(response.json())
```

## Example Response

```json
{
  "highlight": {
    "highlight_id": "17987606483520330",
    "title": "Football 🏈",
    "media_count": 4,
    "cover_url": "https://scontent.cdninstagram.com/v/t51.82787-15/cover.jpg",
    "created_at": "2023-10-24 03:48:13",
    "created_at_timestamp": 1698114493,
    "updated_at": "2023-10-24 03:51:23",
    "updated_at_timestamp": 1698114683,
    "is_pinned": false,
    "url": "https://instagram.com/stories/highlights/17987606483520330/",
    "author": "mrbeast",
    "author_id": "2278169415"
  },
  "stories": [
    {
      "title": "@mrbeast on Instagram",
      "url": "https://instagram.com/stories/mrbeast/3219347044383400902/",
      "date": "2023-10-22 17:34:53",
      "date_timestamp": 1697996093,
      "expires_at": "",
      "expires_at_timestamp": null,
      "author": "mrbeast",
      "author_id": "2278169415",
      "author_name": "MrBeast",
      "author_verified": true,
      "source": "Instagram",
      "domain": "instagram.com",
      "snippet": "",
      "is_video": false,
      "media_type": "story",
      "media_id": "3219347044383400902",
      "thumbnail_url": "https://scontent.cdninstagram.com/v/t51.82787-15/story.jpg",
      "video_url": "",
      "video_duration": null,
      "width": 1284,
      "height": 2282,
      "location": null,
      "tagged_users": [],
      "mentions": [
        "buccaneers"
      ],
      "links": [],
      "audio": null,
      "coauthors": [],
      "is_paid_partnership": false
    }
  ],
  "count": 4
}
```

## Notes

- Get `highlight_id` from the [User Highlights](/docs/instagram-user-highlights) endpoint. Highlight stories do not expire, so `expires_at` is empty.
- Media URLs are temporary CDN links that expire after roughly 6-24 hours.
