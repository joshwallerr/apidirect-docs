# Reddit User Profile

Get a Reddit user's profile by username or profile URL. Returns display name, followers, post and comment counts, post, comment and award karma, bio, avatar and banner, account creation date, and verified, Premium, moderator and employee flags.

## Endpoint

```
GET /v1/reddit/user
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Reddit username, with or without `u/` (3-20 characters). Provide exactly one of `username` or `url`. |
| `url` | One required | Reddit profile URL, e.g. `https://www.reddit.com/user/spez` (max 500 characters). Provide exactly one of `username` or `url`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `user` | object | The user's profile |
| `user.username` | string | Reddit username |
| `user.display_name` | string | Display name shown on the profile, or empty string |
| `user.user_id` | string | Reddit user ID |
| `user.description` | string | Profile bio |
| `user.follower_count` | integer/null | Followers as Reddit reports them. Reddit returns 0 for many accounts, including well-known ones, so treat 0 as unknown (null when unavailable) |
| `user.post_count` | integer/null | Number of posts the user has made (null when unavailable) |
| `user.comment_count` | integer/null | Number of comments the user has made (null when unavailable) |
| `user.link_karma` | integer | Karma from posts |
| `user.comment_karma` | integer | Karma from comments |
| `user.total_karma` | integer | Total karma |
| `user.awardee_karma` | integer | Karma from awards received |
| `user.awarder_karma` | integer | Karma from awards given |
| `user.has_verified_email` | boolean | Whether the account has a verified email |
| `user.verified` | boolean | Whether the account is verified |
| `user.is_gold` | boolean | Whether the user has Reddit Premium |
| `user.is_mod` | boolean | Whether the user moderates at least one subreddit |
| `user.is_employee` | boolean | Whether the user is a Reddit employee |
| `user.nsfw` | boolean | Whether the profile is marked NSFW |
| `user.icon_img` | string | Avatar URL |
| `user.banner_img` | string | Profile banner URL, or empty string |
| `user.created_at` | string | Account creation date and time (UTC) |
| `user.url` | string | Link to the profile |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/user?username=GallowBoob" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/user",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "username": "GallowBoob"
    }
)
print(response.json())
```

## Example Response

```json
{
  "user": {
    "username": "GallowBoob",
    "display_name": "Rob",
    "user_id": "iqsg6",
    "description": "The internet was a mistake 🌍 Always remember the human.",
    "follower_count": 33918,
    "post_count": 12730,
    "comment_count": 14642,
    "link_karma": 35727417,
    "comment_karma": 1110838,
    "total_karma": 36838255,
    "awardee_karma": 0,
    "awarder_karma": 0,
    "has_verified_email": true,
    "verified": true,
    "is_gold": true,
    "is_mod": true,
    "is_employee": false,
    "nsfw": false,
    "icon_img": "https://styles.redditmedia.com/t5_3kl0d/styles/profileIcon_c4zmya3oel6h1.png?width=256&height=256&crop=256:256,smart&s=e339a74eeb89afda40e7d2e7e8bcff8fa0437e94",
    "banner_img": "https://styles.redditmedia.com/t5_3kl0d/styles/profileBanner_74ugoeyr5nif1.png?width=1280&height=384&crop=1280:384,smart&s=89d5e4516ff52160adb45cb005bf49402dbbfcc1",
    "created_at": "2014-10-07 09:38:40",
    "url": "https://www.reddit.com/user/GallowBoob"
  }
}
```
