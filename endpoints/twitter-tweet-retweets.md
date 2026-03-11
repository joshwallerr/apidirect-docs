# Twitter Tweet Retweets

Get the users who retweeted a specific tweet. Returns profile details for each user who retweeted. Supports pagination.

## Endpoint

```
GET /v1/twitter/tweet/retweets
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `tweet_id` | Yes | Numeric tweet ID |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `retweets` | array | Array of user profiles who retweeted |
| `retweets[].username` | string | Twitter username |
| `retweets[].name` | string | Display name |
| `retweets[].user_id` | string | Twitter user ID |
| `retweets[].description` | string | Bio / profile description |
| `retweets[].followers_count` | integer | Number of followers |
| `retweets[].following_count` | integer | Number of accounts followed |
| `retweets[].tweet_count` | integer | Total tweets posted |
| `retweets[].verified` | boolean | Whether verified |
| `retweets[].profile_image_url` | string | URL to profile image |
| `retweets[].created_at` | string | Account creation date |
| `retweets[].url` | string | Link to their profile |
| `tweet_id` | string | Requested tweet ID |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/tweet/retweets?tweet_id=1631781099415257088&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/tweet/retweets",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"tweet_id": "1631781099415257088", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "retweets": [
    {
      "username": "user123",
      "name": "Example User",
      "user_id": "123456789",
      "description": "Retweeted this!",
      "followers_count": 1000,
      "following_count": 500,
      "tweet_count": 3000,
      "verified": false,
      "profile_image_url": "https://pbs.twimg.com/profile_images/.../photo.jpg",
      "created_at": "2019-05-20 08:15:00",
      "url": "https://twitter.com/user123"
    }
  ],
  "tweet_id": "1631781099415257088",
  "pages": 1,
  "count": 20
}
```
