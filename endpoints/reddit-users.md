# Reddit Users

Search Reddit users by keyword. Returns profile data including username, karma scores, account age, bio, and moderation status.

## Endpoint

```
GET /v1/reddit/users
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `users` | array | Array of matching user profiles |
| `users[].username` | string | Reddit username |
| `users[].user_id` | string | Reddit user ID |
| `users[].description` | string | Profile bio / description |
| `users[].link_karma` | integer | Karma from posts |
| `users[].comment_karma` | integer | Karma from comments |
| `users[].total_karma` | integer | Combined post and comment karma |
| `users[].has_verified_email` | boolean | Whether the user has a verified email |
| `users[].is_gold` | boolean | Whether the user has Reddit Premium |
| `users[].is_mod` | boolean | Whether the user is a moderator |
| `users[].icon_img` | string | URL to profile avatar |
| `users[].created_at` | string/null | Account creation date |
| `users[].url` | string | Link to the profile |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/users?query=programming" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/users",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "programming"}
)
print(response.json())
```

## Example Response

```json
{
  "users": [
    {
      "username": "spez",
      "user_id": "1w72",
      "description": "CEO of Reddit",
      "link_karma": 148670,
      "comment_karma": 650342,
      "total_karma": 799012,
      "has_verified_email": true,
      "is_gold": true,
      "is_mod": true,
      "icon_img": "https://styles.redditmedia.com/...",
      "created_at": "2005-06-06 04:00:00",
      "url": "https://reddit.com/user/spez"
    }
  ],
  "count": 25
}
```
