# Twitter User Following

Get the accounts that a specific Twitter/X user is following. Returns profile details for each followed account. Supports pagination.

## Endpoint

```
GET /v1/twitter/user/following
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
| `following` | array | Array of followed user profiles |
| `following[].username` | string | Twitter username |
| `following[].name` | string | Display name |
| `following[].user_id` | string | Twitter user ID |
| `following[].description` | string | Bio / profile description |
| `following[].followers_count` | integer | Number of followers they have |
| `following[].following_count` | integer | Number of accounts they follow |
| `following[].tweet_count` | integer | Total tweets posted |
| `following[].verified` | boolean | Whether they are verified |
| `following[].profile_image_url` | string | URL to profile image |
| `following[].created_at` | string | Account creation date |
| `following[].url` | string | Link to their profile |
| `username` | string | Requested username |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/user/following?username=elonmusk&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/user/following",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "elonmusk", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "following": [
    {
      "username": "SpaceX",
      "name": "SpaceX",
      "user_id": "34743251",
      "description": "SpaceX designs, manufactures and launches...",
      "followers_count": 35000000,
      "following_count": 50,
      "tweet_count": 5000,
      "verified": true,
      "profile_image_url": "https://pbs.twimg.com/profile_images/.../photo.jpg",
      "created_at": "2009-04-23 19:30:00",
      "url": "https://twitter.com/SpaceX"
    }
  ],
  "username": "elonmusk",
  "pages": 1,
  "count": 20
}
```
