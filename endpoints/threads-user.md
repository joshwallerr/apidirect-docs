# Threads User Profile

Get the full profile for a single Threads user by username. Returns biography, follower count, verification status, profile picture (standard and high resolution), the external bio links displayed on the profile, and the topic tags shown on the profile.

## Endpoint

```
GET /v1/threads/user
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | Yes | Threads username, with or without leading @ (max 100 characters) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `user` | object | Profile data object |
| `user.username` | string | Threads username |
| `user.full_name` | string | Display name |
| `user.user_id` | string | Threads user ID |
| `user.biography` | string | Profile biography text |
| `user.follower_count` | integer | Number of followers |
| `user.is_verified` | boolean | Whether the user is verified |
| `user.is_private` | boolean | Whether the account is private |
| `user.profile_pic_url` | string | URL to standard-resolution profile picture |
| `user.profile_pic_url_hd` | string | URL to high-resolution profile picture |
| `user.bio_links` | array | External bio link objects shown on the profile (`url`, `title`); empty array when the profile has no links |
| `user.profile_tags` | array | Topic tags shown on the profile (`name`, `display_name`); empty array when none |
| `user.url` | string | Link to the profile |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/threads/user?username=zuck" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/threads/user",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "zuck"}
)
print(response.json())
```

## Example Response

```json
{
  "user": {
    "username": "zuck",
    "full_name": "Mark Zuckerberg",
    "user_id": "63055343223",
    "biography": "Mostly superintelligence and MMA takes",
    "follower_count": 5673124,
    "is_verified": true,
    "is_private": false,
    "profile_pic_url": "https://scontent.cdninstagram.com/.../photo.jpg",
    "profile_pic_url_hd": "https://scontent.cdninstagram.com/.../photo_640x640.jpg",
    "bio_links": [
      {"url": "https://www.meta.com", "title": "meta.com"}
    ],
    "profile_tags": [
      {"name": "aithreads", "display_name": "AI Threads"}
    ],
    "url": "https://www.threads.com/@zuck"
  }
}
```