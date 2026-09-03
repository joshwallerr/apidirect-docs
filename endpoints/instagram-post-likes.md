# Instagram Post Likes

Get the users who liked an Instagram post or reel by URL or shortcode. Returns username, full name, user ID, verification status, and profile picture for each liker, plus the post's total like count.

## Endpoint

```
GET /v1/instagram/post/likes
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Instagram post or reel URL, e.g. `https://www.instagram.com/p/CxYQJO8xuC6/` (max 500 characters). Provide either `url` or `code`. |
| `code` | One required | The post's shortcode, e.g. `CxYQJO8xuC6`, or numeric media ID (max 50 characters). Provide either `url` or `code`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `likes` | array | Array of users who liked the post |
| `likes[].username` | string | Instagram username |
| `likes[].full_name` | string | Display name |
| `likes[].user_id` | string | Instagram user ID |
| `likes[].is_verified` | boolean | Whether the user is verified (blue checkmark) |
| `likes[].is_private` | boolean | Whether the account is private |
| `likes[].profile_pic_url` | string | URL to profile picture |
| `likes[].url` | string | Link to the profile |
| `code` | string | The post's shortcode (or media ID, if that was passed) |
| `total` | integer | The post's total like count |
| `count` | integer | Number of likers returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/post/likes?code=CxYQJO8xuC6" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/post/likes",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "code": "CxYQJO8xuC6"
    }
)
print(response.json())
```

## Example Response

```json
{
  "likes": [
    {
      "username": "grannyfeet9",
      "full_name": "Feetgranny",
      "user_id": "25641676135",
      "is_verified": false,
      "is_private": true,
      "profile_pic_url": "https://scontent.cdninstagram.com/v/t51.2885-19/photo.jpg",
      "url": "https://instagram.com/grannyfeet9"
    }
  ],
  "code": "CxYQJO8xuC6",
  "total": 182068,
  "count": 845
}
```

## Notes

- One request returns every liker Instagram exposes (typically several hundred). `total` is the post's full like count.
