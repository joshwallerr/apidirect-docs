# Twitter Users

Search Twitter/X users by keyword. Returns profile data including username, display name, bio, follower/following counts, verification status, and profile image. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/twitter/users
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
| `users[].username` | string | Twitter username (handle) |
| `users[].name` | string | Display name |
| `users[].user_id` | string | Twitter user ID |
| `users[].description` | string | Bio / profile description |
| `users[].followers_count` | integer | Number of followers |
| `users[].following_count` | integer | Number of accounts followed |
| `users[].tweet_count` | integer | Total tweets posted |
| `users[].verified` | boolean | Whether the user is verified (blue checkmark) |
| `users[].profile_image_url` | string | URL to profile image |
| `users[].created_at` | string/null | Account creation date |
| `users[].url` | string | Link to the profile |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/users?query=AI&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/users",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "AI",
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
      "username": "OpenAI",
      "name": "OpenAI",
      "user_id": "4398626122",
      "description": "Creating safe AGI that benefits all of humanity.",
      "followers_count": 3842150,
      "following_count": 0,
      "tweet_count": 2145,
      "verified": true,
      "profile_image_url": "https://pbs.twimg.com/profile_images/.../photo.jpg",
      "created_at": "2015-12-09 20:42:45",
      "url": "https://twitter.com/OpenAI"
    }
  ],
  "pages": 1,
  "count": 20
}
```
