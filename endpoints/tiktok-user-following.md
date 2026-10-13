# TikTok User Following

Get the accounts a user follows, by username, numeric user ID, or profile URL. Returns the same profile fields as User Followers for each account, 50 per page. Accounts that hide their following list return 403.

## Endpoint

```
GET /v1/tiktok/user/following
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `username`, `user_id`, or `url`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | TikTok username, with or without leading `@` (max 100 characters). |
| `user_id` | One required | Numeric TikTok user ID, as returned by [Search Users](/docs/tiktok-users) or [User Profile](/docs/tiktok-user). |
| `url` | One required | TikTok profile URL, e.g. `https://www.tiktok.com/@tiktok` (max 500 characters). |
| `pages` | No | Number of pages to fetch, 1-1000 (default: 1). Each page returns up to 50 accounts. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `following` | array | Array of the accounts the user follows |
| `following[].username` | string | TikTok username (unique ID) |
| `following[].nickname` | string | Display name |
| `following[].user_id` | string | TikTok user ID |
| `following[].sec_uid` | string | TikTok secondary user ID (secUid) |
| `following[].bio` | string | Profile bio / signature |
| `following[].verified` | boolean | Whether the user is verified |
| `following[].is_private` | boolean | Whether the account is private |
| `following[].followers` | integer | Number of followers |
| `following[].following` | integer | Number of accounts followed |
| `following[].likes` | integer | Total likes received |
| `following[].video_count` | integer | Number of videos posted |
| `following[].videos_liked` | integer | Number of videos the user has liked |
| `following[].avatar` | string | URL to profile picture |
| `following[].region` | string | 2-letter region code of the account |
| `following[].language` | string | Account language code |
| `following[].date_joined` | string | Date and time the account was created |
| `following[].date_joined_timestamp` | integer/null | Unix timestamp of the account creation date |
| `following[].instagram_username` | string | Linked Instagram username, or empty string |
| `following[].twitter_id` | string | Linked X/Twitter account ID, or empty string |
| `following[].twitter_username` | string | Linked X/Twitter username, or empty string |
| `following[].youtube_channel_id` | string | Linked YouTube channel ID, or empty string |
| `following[].youtube_channel_title` | string | Linked YouTube channel name, or empty string |
| `following[].url` | string | Link to the profile |
| `username` | string | The requested username (empty when looked up by user_id) |
| `user_id` | string | The user's numeric ID |
| `total` | integer | The user's total following count |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

An account that hides its following list returns a `403` with `code: "limited_account"`.

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/user/following?username=gordonramsayofficial&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/user/following",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "username": "gordonramsayofficial",
        "pages": 2
    }
)
print(response.json())
```

## Example Response

```json
{
  "following": [
    {
      "username": "netflixuk",
      "nickname": "NetflixUK",
      "user_id": "6796949557193655302",
      "sec_uid": "MS4wLjABAAAAQp_PoXccOVClw6n4sGzXVXdr3W92EtzhdlaZeE...",
      "bio": "🐝",
      "verified": true,
      "is_private": false,
      "followers": 2238486,
      "following": 41,
      "likes": 95184771,
      "video_count": 1614,
      "videos_liked": 1723,
      "avatar": "https://p19-common-sign.tiktokcdn.com/.../avatar.jpeg",
      "region": "GB",
      "language": "en",
      "date_joined": "2020-02-24 01:58:52",
      "date_joined_timestamp": 1582509532,
      "instagram_username": "",
      "twitter_id": "",
      "twitter_username": "",
      "youtube_channel_id": "",
      "youtube_channel_title": "",
      "url": "https://www.tiktok.com/@netflixuk"
    }
  ],
  "username": "gordonramsayofficial",
  "user_id": "6747935906352907269",
  "total": 555,
  "pages": 2,
  "count": 100
}
```
