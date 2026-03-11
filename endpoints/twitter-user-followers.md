# Twitter User Followers

Get the followers of a specific Twitter/X user. Returns profile details for each follower including username, bio, follower counts, and verification status. Supports pagination.

## Endpoint

```
GET /v1/twitter/user/followers
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | Yes | Twitter username (without @, max 50 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `followers` | array | Array of follower profiles |
| `followers[].username` | string | Follower's Twitter username |
| `followers[].name` | string | Display name |
| `followers[].user_id` | string | Twitter user ID |
| `followers[].description` | string | Bio / profile description |
| `followers[].followers_count` | integer | Number of followers they have |
| `followers[].following_count` | integer | Number of accounts they follow |
| `followers[].tweet_count` | integer | Total tweets posted |
| `followers[].verified` | boolean | Whether they are verified |
| `followers[].profile_image_url` | string | URL to profile image |
| `followers[].created_at` | string | Account creation date |
| `followers[].url` | string | Link to their profile |
| `username` | string | Requested username |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/user/followers?username=elonmusk&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/user/followers",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "elonmusk", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "followers": [
    {
      "username": "user123",
      "name": "Example User",
      "user_id": "123456789",
      "description": "Tech enthusiast",
      "followers_count": 5000,
      "following_count": 200,
      "tweet_count": 1500,
      "verified": false,
      "profile_image_url": "https://pbs.twimg.com/profile_images/.../photo.jpg",
      "created_at": "2020-01-15 10:30:00",
      "url": "https://twitter.com/user123"
    }
  ],
  "username": "elonmusk",
  "pages": 1,
  "count": 20
}
```
