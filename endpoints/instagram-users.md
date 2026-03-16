# Instagram Users

Search Instagram users by keyword. Returns username, full name, user ID, verification status, privacy status, and profile picture URL.

## Endpoint

```
GET /v1/instagram/users
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `users` | array | Array of matching user profiles |
| `users[].username` | string | Instagram username |
| `users[].full_name` | string | Display name |
| `users[].user_id` | string | Instagram user ID |
| `users[].is_verified` | boolean | Whether the user is verified (blue checkmark) |
| `users[].is_private` | boolean | Whether the account is private |
| `users[].profile_pic_url` | string | URL to profile picture |
| `users[].url` | string | Link to the profile |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/users?query=photography" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/users",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "photography"}
)
print(response.json())
```

## Example Response

```json
{
  "users": [
    {
      "username": "natgeo",
      "full_name": "National Geographic",
      "user_id": "787132",
      "is_verified": true,
      "is_private": false,
      "profile_pic_url": "https://scontent.cdninstagram.com/.../photo.jpg",
      "url": "https://instagram.com/natgeo"
    }
  ],
  "count": 50
}
```
