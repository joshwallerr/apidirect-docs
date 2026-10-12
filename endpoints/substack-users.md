# Search Substack Users

Search Substack authors and publication profiles by name or keyword. Returns handle, display name, bio, follower count, subscriber badge, bestseller tier and primary publication for each profile.

## Endpoint

```
GET /v1/substack/users
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `page` | No | Page number, 1-4 (default: 1). 20 profiles per page |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `users` | array | Array of matching profiles |
| `users[].username` | string | Substack handle |
| `users[].full_name` | string | Display name |
| `users[].user_id` | string | User ID (pass it as `user_id` to the user endpoints) |
| `users[].biography` | string | Profile bio |
| `users[].profile_pic_url` | string | Profile picture URL |
| `users[].follower_count` | integer | Number of followers |
| `users[].subscriber_count` | integer | Rounded subscriber count of the primary publication, 0 when not shown |
| `users[].subscriber_count_label` | string | The displayed subscriber badge, e.g. `1.2M+` |
| `users[].bestseller_tier` | integer | Bestseller badge tier: 0, 100, 1000 or 10000 |
| `users[].is_bestseller` | boolean | Whether the author carries a bestseller badge |
| `users[].paid_subscriber_band` | string | Paid subscriber band of the primary publication, e.g. `Tens of thousands`, empty when not shown |
| `users[].paid_subscriber_floor` | integer | Lower bound of the paid band (100, 1000, 10000), 0 when none |
| `users[].leaderboard` | object/null | Leaderboard placement (`category`, `category_id`, `rank`, `board`), null when unranked |
| `users[].twitter_handle` | string | X handle, empty when none |
| `users[].primary_publication` | object/null | The author's main publication (`publication_id`, `name`, `subdomain`, `url`, `logo_url`) |
| `users[].date_joined` | string | Profile creation date and time (UTC) |
| `users[].url` | string | Link to the profile |
| `query` | string | The search keyword |
| `page` | integer | Current page number |
| `has_next_page` | boolean | Whether another page exists |
| `count` | integer | Number of profiles returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/users?query=lenny&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/users",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "lenny", "page": 1}
)
print(response.json())
```

## Example Response

```json
{
  "count": 20,
  "has_next_page": true,
  "page": 1,
  "query": "lenny",
  "users": [
    {
      "bestseller_tier": 10000,
      "biography": "Writing • Angel investing • Advising",
      "date_joined": "2021-05-01 23:55:21",
      "follower_count": 1383966,
      "full_name": "Lenny Rachitsky",
      "is_bestseller": true,
      "leaderboard": {
        "board": "paid",
        "category": "Business",
        "category_id": 62,
        "rank": 1
      },
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
      "subscriber_count": 1200000,
      "subscriber_count_label": "1.2M+",
      "twitter_handle": "lennysan",
      "url": "https://substack.com/@lenny",
      "user_id": "1849774",
      "username": "lenny"
    }
  ]
}
```
