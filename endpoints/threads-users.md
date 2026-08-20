# Threads Search Users

Search Threads users by keyword. Returns username, display name, user ID, verification status, privacy status, and profile picture URL.

## Endpoint

```
GET /v1/threads/users
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
| `users[].username` | string | Threads username |
| `users[].full_name` | string | Display name |
| `users[].user_id` | string | Threads user ID |
| `users[].is_verified` | boolean | Whether the user is verified |
| `users[].is_private` | boolean | Whether the account is private |
| `users[].profile_pic_url` | string | URL to profile picture |
| `users[].url` | string | Link to the profile |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/threads/users?query=technology" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/threads/users",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "technology"}
)
print(response.json())
```

## Example Response

```json
{
  "users": [
    {
      "username": "technologyreview",
      "full_name": "MIT Technology Review",
      "user_id": "63213270539",
      "is_verified": true,
      "is_private": false,
      "profile_pic_url": "https://scontent.cdninstagram.com/.../photo.jpg",
      "url": "https://www.threads.com/@technologyreview"
    }
  ],
  "count": 9
}
```

## Notes

- Search Users returns basic discovery data only. For a full profile — biography, follower count, and bio links — use the [User Profile](/docs/threads-user) endpoint.
- Each request returns a single page of matching users (typically up to 15).