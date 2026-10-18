# Reddit Users

Search Reddit users by keyword. Returns profile data including username, karma scores, account age, bio, banner, and verified, moderator, employee and NSFW flags. Up to 100 users, 25 per page.

## Endpoint

```
GET /v1/reddit/users
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-4 (default: 1). Each page returns up to 25 users. |

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
| `users[].verified` | boolean | Whether the account is verified |
| `users[].is_gold` | boolean | Whether the user has Reddit Premium |
| `users[].is_mod` | boolean | Whether the user is a moderator |
| `users[].is_employee` | boolean | Whether the user is a Reddit employee |
| `users[].nsfw` | boolean | Whether the profile is marked NSFW |
| `users[].icon_img` | string | URL to profile avatar |
| `users[].banner_img` | string | Profile banner URL, or empty string |
| `users[].created_at` | string/null | Account creation date |
| `users[].url` | string | Link to the profile |
| `pages` | integer | Number of pages returned |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/users?query=programming&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/users",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "programming", "pages": 2}
)
print(response.json())
```

## Example Response

```json
{
  "users": [
    {
      "username": "FrequencyProgramming",
      "user_id": "5btdelnr",
      "description": "Our moto is simply to spread positive energy and thoughts all over the world. Our music generally helps to enhance positive energy and relax the mind/body/so...",
      "link_karma": 563,
      "comment_karma": 167,
      "total_karma": 730,
      "has_verified_email": true,
      "verified": true,
      "is_gold": false,
      "is_mod": false,
      "is_employee": false,
      "nsfw": false,
      "icon_img": "https://styles.redditmedia.com/t5_2bjoel/styles/profileIcon_hrd7fh726c941.jpg?width=256&height=256&crop=256:256,smart&s=87813f382b26c26c6d79f01425814bd54931273e",
      "banner_img": "https://styles.redditmedia.com/t5_2bjoel/styles/profileBanner_s18l62qo6c941.jpg?width=1280&height=384&crop=1280:384,smart&s=aaffe2423335ba6ced9b97b696ad39c0afe628f9",
      "created_at": "2019-12-29 19:24:22",
      "url": "https://reddit.com/user/FrequencyProgramming"
    }
  ],
  "pages": 2,
  "count": 32
}
```
