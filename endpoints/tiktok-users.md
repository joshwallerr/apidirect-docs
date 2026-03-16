# TikTok Users

Search TikTok users by keyword. Returns username, nickname, bio, follower/following counts, total likes, video count, and verification status. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/tiktok/users
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `users` | array | Array of matching user profiles |
| `users[].username` | string | TikTok username (unique ID) |
| `users[].nickname` | string | Display name |
| `users[].user_id` | string | TikTok user ID |
| `users[].bio` | string | Profile bio / signature |
| `users[].verified` | boolean | Whether the user is verified |
| `users[].is_private` | boolean | Whether the account is private |
| `users[].followers` | integer | Number of followers |
| `users[].following` | integer | Number of accounts followed |
| `users[].likes` | integer | Total likes received |
| `users[].video_count` | integer | Number of videos posted |
| `users[].avatar` | string | URL to profile picture |
| `users[].url` | string | Link to the profile |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/users?query=cooking&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/users",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "cooking",
        "pages": 1
    }
)
print(response.json())
```

## Example Response

```json
{
  "users": [
    {
      "username": "cookingwithshereen",
      "nickname": "Shereen Pavlides",
      "user_id": "6812601268610257926",
      "bio": "Chef | Author | TV Host",
      "verified": true,
      "is_private": false,
      "followers": 483313,
      "following": 47,
      "likes": 3090163,
      "video_count": 728,
      "avatar": "https://p16-sign.tiktokcdn-us.com/.../photo.webp",
      "url": "https://www.tiktok.com/@cookingwithshereen"
    }
  ],
  "pages": 1,
  "count": 30
}
```
