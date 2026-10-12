# Substack User Profile

Get a Substack author's full profile by handle, user ID or profile URL. Returns display name, bio, follower count, subscriber badge, bestseller tier, the publications they write for, profile links, X handle and leaderboard placement and the publications they subscribe to.

## Endpoint

```
GET /v1/substack/user
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

Provide exactly one of `username`, `user_id` or `url`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Substack handle, e.g. `lenny`, with or without a leading `@` (max 100 characters). Provide one of `username`, `user_id` or `url`. |
| `user_id` | One required | Numeric Substack user ID, as returned in `user_id`. Provide one of `username`, `user_id` or `url`. |
| `url` | One required | Profile URL, e.g. `https://substack.com/@lenny` (max 500 characters). Provide one of `username`, `user_id` or `url`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `user` | object | Profile data |
| `user.username` | string | Substack handle |
| `user.full_name` | string | Display name |
| `user.user_id` | string | User ID (pass it as `user_id` to the user endpoints) |
| `user.biography` | string | Profile bio |
| `user.profile_pic_url` | string | Profile picture URL |
| `user.follower_count` | integer | Number of followers |
| `user.subscriber_count` | integer | Rounded subscriber count of the primary publication, 0 when not shown |
| `user.subscriber_count_label` | string | The displayed subscriber badge, e.g. `1.2M+` |
| `user.bestseller_tier` | integer | Bestseller badge tier: 0, 100, 1000 or 10000 |
| `user.is_bestseller` | boolean | Whether the author carries a bestseller badge |
| `user.paid_subscriber_band` | string | Paid subscriber band of the primary publication, e.g. `Tens of thousands`, empty when not shown |
| `user.paid_subscriber_floor` | integer | Lower bound of the paid band (100, 1000, 10000), 0 when none |
| `user.primary_publication` | object/null | The author's main publication (`publication_id`, `name`, `subdomain`, `url`, `logo_url`) |
| `user.date_joined` | string | Profile creation date and time (UTC) |
| `user.url` | string | Link to the profile |
| `user.publications` | array | Publications the author writes for (`publication_id`, `name`, `subdomain`, `url`, `logo_url`, `role`) |
| `user.links` | array | Links on the profile (`type`, `label`, `url`) |
| `user.twitter_handle` | string | Connected X handle, empty when none |
| `user.leaderboard` | object/null | Leaderboard placement (`category`, `category_id`, `rank`, `board`), or null |
| `user.subscriptions_count` | integer | Number of publications the author publicly subscribes to |
| `user.slug` | string | Profile slug, as in `substack.com/profile/<id>-<slug>` |
| `user.recommendation_count` | integer | Number of publications the author's primary publication recommends |
| `user.has_guest_posts` | boolean | Whether the author has guest posts on other publications |
| `user.subscriptions` | array | The publications the author publicly subscribes to (`publication_id`, `name`, `subdomain`, `url`, `logo_url`, `plan`) |
| `user.subscriptions[].plan` | string | `free`, `paid` or `comp` (a complimentary paid subscription) |
| `user.has_posts` | boolean | Whether the author has published posts |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/user?username=lenny" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/user",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "lenny"}
)
print(response.json())
```

## Example Response

```json
{
  "user": {
    "bestseller_tier": 10000,
    "biography": "Writing • Angel investing • Advising",
    "date_joined": "2021-05-01 23:55:21",
    "follower_count": 1383966,
    "full_name": "Lenny Rachitsky",
    "has_guest_posts": true,
    "has_posts": true,
    "is_bestseller": true,
    "leaderboard": {
      "board": "paid",
      "category": "Business",
      "category_id": 62,
      "rank": 1
    },
    "links": [
      {
        "label": "",
        "type": "twitter",
        "url": "https://x.com/lennysan"
      }
    ],
    "paid_subscriber_band": "Tens of thousands",
    "paid_subscriber_floor": 10000,
    "primary_publication": {
      "logo_url": "https://substack-post-media.s3.amazonaws.com/public/images/441213db-4824-4e48-9d28-a3a18952cbfc_592x592.png",
      "name": "Lenny's Newsletter",
      "publication_id": "10845",
      "subdomain": "lenny",
      "url": "https://www.lennysnewsletter.com"
    },
    "profile_pic_url": "https://bucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com/public/images/afba5161-65bb-4d99-8d6b-cce660917fa1_1540x1540.png",
    "publications": [
      {
        "logo_url": "https://substack-post-media.s3.amazonaws.com/public/images/441213db-4824-4e48-9d28-a3a18952cbfc_592x592.png",
        "name": "Lenny's Newsletter",
        "publication_id": "10845",
        "role": "admin",
        "subdomain": "lenny",
        "url": "https://www.lennysnewsletter.com"
      }
    ],
    "recommendation_count": 11,
    "slug": "lenny-rachitsky",
    "subscriber_count": 1200000,
    "subscriber_count_label": "1.2M+",
    "subscriptions": [
      {
        "logo_url": "https://substack-post-media.s3.amazonaws.com/public/images/cc7ca458-37ff-4275-a738-d25e07f498c2_1280x1280.png",
        "name": "@jasmine’s substack",
        "plan": "paid",
        "publication_id": "6027",
        "subdomain": "jasmine",
        "url": "https://jasmi.news"
      }
    ],
    "subscriptions_count": 109,
    "twitter_handle": "lennysan",
    "url": "https://substack.com/@lenny",
    "user_id": "1849774",
    "username": "lenny"
  }
}
```
