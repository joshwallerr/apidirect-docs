# Instagram User Highlights

Get a user's story highlights by username or profile URL. Returns each highlight's ID, title, story count, cover image, and dates.

## Endpoint

```
GET /v1/instagram/user/highlights
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
| `highlights` | array | Array of the user's story highlights, most recently updated first |
| `highlights[].highlight_id` | string | Highlight ID (use with the Highlight Stories endpoint) |
| `highlights[].title` | string | Highlight title |
| `highlights[].media_count` | integer | Number of stories in the highlight |
| `highlights[].cover_url` | string | Cover image URL (temporary; valid ~6-24 hours) |
| `highlights[].created_at` | string | Creation date and time |
| `highlights[].created_at_timestamp` | integer/null | Creation date as a Unix timestamp |
| `highlights[].updated_at` | string | Date and time a story was last added |
| `highlights[].updated_at_timestamp` | integer/null | Last-updated date as a Unix timestamp |
| `highlights[].is_pinned` | boolean | Whether the highlight is pinned on the profile |
| `highlights[].url` | string | Direct link to the highlight |
| `highlights[].author` | string | Owner's Instagram username |
| `highlights[].author_id` | string | Owner's Instagram user ID |
| `username` | string | The requested username |
| `count` | integer | Number of highlights returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/user/highlights?username=mrbeast" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/user/highlights",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "username": "mrbeast"
    }
)
print(response.json())
```

## Example Response

```json
{
  "highlights": [
    {
      "highlight_id": "17929440964811872",
      "title": "Operation Chad",
      "media_count": 14,
      "cover_url": "https://scontent.cdninstagram.com/v/t51.82787-15/cover.jpg",
      "created_at": "2021-12-01 21:15:33",
      "created_at_timestamp": 1638393333,
      "updated_at": "2025-08-09 03:54:16",
      "updated_at_timestamp": 1754706856,
      "is_pinned": false,
      "url": "https://instagram.com/stories/highlights/17929440964811872/",
      "author": "mrbeast",
      "author_id": "2278169415"
    }
  ],
  "username": "mrbeast",
  "count": 9
}
```

## Notes

- Pass `highlight_id` to the [Highlight Stories](/docs/instagram-highlight-stories) endpoint to get the stories inside a highlight.
- An account with no highlights returns an empty `highlights` array. A private account returns `403` with code `private_account`, and a username that does not exist returns `404` with code `not_found`.
