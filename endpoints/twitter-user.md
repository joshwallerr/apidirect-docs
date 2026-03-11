# Twitter User Profile

Get detailed profile information for a Twitter/X user by username. Returns account details, follower/following counts, bio, verification status, and account metadata.

## Endpoint

```
GET /v1/twitter/user
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | Yes | Twitter username (without @, max 50 characters) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `user` | object | User profile data |
| `user.username` | string | Twitter username |
| `user.name` | string | Display name |
| `user.user_id` | string | Twitter user ID (rest_id) |
| `user.description` | string | Bio / profile description |
| `user.url` | string | Link to the profile |
| `user.followers_count` | integer | Number of followers |
| `user.following_count` | integer | Number of accounts followed |
| `user.tweet_count` | integer | Total tweets posted |
| `user.favourites_count` | integer | Total tweets liked |
| `user.listed_count` | integer | Number of lists the user is on |
| `user.media_count` | integer | Number of media posts |
| `user.verified` | boolean | Whether the user is verified (blue checkmark) |
| `user.protected` | boolean | Whether the account is private |
| `user.profile_image_url` | string | URL to profile image (400x400) |
| `user.profile_banner_url` | string | URL to profile banner |
| `user.created_at` | string | Account creation date |
| `user.pinned_tweet_ids` | string[] | IDs of pinned tweets |
| `user.account_based_in` | string | Country the account is based in |
| `user.username_changes` | integer | Number of username changes |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/user?username=elonmusk" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/user",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "elonmusk"}
)
print(response.json())
```

## Example Response

```json
{
  "user": {
    "username": "elonmusk",
    "name": "Elon Musk",
    "user_id": "44196397",
    "description": "",
    "url": "https://twitter.com/elonmusk",
    "followers_count": 235918920,
    "following_count": 1292,
    "tweet_count": 98359,
    "favourites_count": 214306,
    "listed_count": 167743,
    "media_count": 4372,
    "verified": true,
    "protected": false,
    "profile_image_url": "https://pbs.twimg.com/profile_images/.../photo_400x400.jpg",
    "profile_banner_url": "https://pbs.twimg.com/profile_banners/44196397/...",
    "created_at": "2009-06-02 20:12:29",
    "pinned_tweet_ids": ["2028500984977330453"],
    "account_based_in": "United States",
    "username_changes": 0
  }
}
```
