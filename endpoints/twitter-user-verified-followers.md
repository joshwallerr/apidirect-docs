# Twitter Verified Followers

Get the verified (blue checkmark) followers of a specific Twitter/X user. Only returns followers who have a verified account. Supports pagination.

## Endpoint

```
GET /v1/twitter/user/verified-followers
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
| `verified_followers` | array | Array of verified follower profiles |
| `verified_followers[].username` | string | Twitter username |
| `verified_followers[].name` | string | Display name |
| `verified_followers[].user_id` | string | Twitter user ID |
| `verified_followers[].description` | string | Bio / profile description |
| `verified_followers[].followers_count` | integer | Number of followers they have |
| `verified_followers[].following_count` | integer | Number of accounts they follow |
| `verified_followers[].tweet_count` | integer | Total tweets posted |
| `verified_followers[].verified` | boolean | Always `true` for this endpoint |
| `verified_followers[].profile_image_url` | string | URL to profile image |
| `verified_followers[].created_at` | string | Account creation date |
| `verified_followers[].url` | string | Link to their profile |
| `username` | string | Requested username |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/user/verified-followers?username=elonmusk&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/user/verified-followers",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "elonmusk", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "verified_followers": [
    {
      "username": "verified_user",
      "name": "Verified User",
      "user_id": "987654321",
      "description": "Tech CEO",
      "followers_count": 500000,
      "following_count": 300,
      "tweet_count": 10000,
      "verified": true,
      "profile_image_url": "https://pbs.twimg.com/profile_images/.../photo.jpg",
      "created_at": "2018-06-10 14:00:00",
      "url": "https://twitter.com/verified_user"
    }
  ],
  "username": "elonmusk",
  "pages": 1,
  "count": 20
}
```
