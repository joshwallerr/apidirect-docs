# TikTok User Followers

Get a user's followers, newest first, by username, numeric user ID, or profile URL. Returns the username, display name, user ID, bio, follower and following counts, total likes, video count, verification status, region, join date, and linked Instagram, X/Twitter, and YouTube accounts for each follower, 100 per page.

## Endpoint

```
GET /v1/tiktok/user/followers
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
| `pages` | No | Number of pages to fetch, 1-1000 (default: 1). Each page returns up to 100 followers. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `followers` | array | Array of follower profiles, newest first |
| `followers[].username` | string | TikTok username (unique ID) |
| `followers[].nickname` | string | Display name |
| `followers[].user_id` | string | TikTok user ID |
| `followers[].sec_uid` | string | TikTok secondary user ID (secUid) |
| `followers[].bio` | string | Profile bio / signature |
| `followers[].verified` | boolean | Whether the user is verified |
| `followers[].is_private` | boolean | Whether the account is private |
| `followers[].followers` | integer | Number of followers |
| `followers[].following` | integer | Number of accounts followed |
| `followers[].likes` | integer | Total likes received |
| `followers[].video_count` | integer | Number of videos posted |
| `followers[].videos_liked` | integer | Number of videos the user has liked |
| `followers[].avatar` | string | URL to profile picture |
| `followers[].region` | string | 2-letter region code of the account |
| `followers[].language` | string | Account language code |
| `followers[].date_joined` | string | Date and time the account was created |
| `followers[].date_joined_timestamp` | integer/null | Unix timestamp of the account creation date |
| `followers[].instagram_username` | string | Linked Instagram username, or empty string |
| `followers[].twitter_id` | string | Linked X/Twitter account ID, or empty string |
| `followers[].twitter_username` | string | Linked X/Twitter username, or empty string |
| `followers[].youtube_channel_id` | string | Linked YouTube channel ID, or empty string |
| `followers[].youtube_channel_title` | string | Linked YouTube channel name, or empty string |
| `followers[].url` | string | Link to the profile |
| `username` | string | The requested username (empty when looked up by user_id) |
| `user_id` | string | The user's numeric ID |
| `total` | integer | The user's total follower count |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

A private account hides its followers list and returns a `403` with `code: "limited_account"`.

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/user/followers?username=tiktok&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/user/followers",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "username": "tiktok",
        "pages": 2
    }
)
print(response.json())
```

## Example Response

```json
{
  "followers": [
    {
      "username": "sasuke_xp51",
      "nickname": "sasuke",
      "user_id": "7694873557775795208",
      "sec_uid": "MS4wLjABAAAAy5zt1DSVO2SBG4_L3zBwLNblfaiILoOJeio3WU...",
      "bio": "",
      "verified": false,
      "is_private": false,
      "followers": 2,
      "following": 5,
      "likes": 0,
      "video_count": 0,
      "videos_liked": 191,
      "avatar": "https://p19-common-sign.tiktokcdn.com/.../avatar.jpeg",
      "region": "TH",
      "language": "th",
      "date_joined": "2026-10-10 03:19:47",
      "date_joined_timestamp": 1791602387,
      "instagram_username": "",
      "twitter_id": "",
      "twitter_username": "",
      "youtube_channel_id": "",
      "youtube_channel_title": "",
      "url": "https://www.tiktok.com/@sasuke_xp51"
    }
  ],
  "username": "tiktok",
  "user_id": "107955",
  "total": 96206555,
  "pages": 2,
  "count": 200
}
```
