# Facebook Page Details

Get detailed information about a Facebook page by URL. Returns the page name, ID, follower/like counts, categories, contact info, rating, and more.

## Endpoint

```
GET /v1/facebook/page
```

**Price:** $0.008 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | Facebook page URL (e.g. https://www.facebook.com/facebook) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `page` | object | Page profile data |
| `page.name` | string | Page display name |
| `page.page_id` | string | Facebook page ID |
| `page.url` | string | URL of the page |
| `page.type` | string | Page type (e.g. "Company") |
| `page.image` | string | URL to page profile image |
| `page.cover_image` | string | URL to page cover image |
| `page.followers` | integer | Number of followers |
| `page.likes` | integer | Number of page likes |
| `page.following` | integer | Number of accounts the page follows |
| `page.categories` | string[] | List of page categories |
| `page.intro` | string | Short intro / about text |
| `page.website` | string | Website URL listed on the page |
| `page.phone` | string | Phone number listed on the page |
| `page.email` | string | Email address listed on the page |
| `page.address` | string | Physical address listed on the page |
| `page.rating` | number | Average page rating (out of 5) |
| `page.price_range` | string | Price range indicator (e.g. "$$") |
| `page.verified` | boolean | Whether the page is verified |
| `page.delegate_page_id` | string | Delegate page ID (used for videos endpoint) |
| `page.reels_page_id` | string | Reels page ID (used for reels endpoint) |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/page?url=https://www.facebook.com/facebook" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/page",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.facebook.com/facebook"}
)
print(response.json())
```

## Example Response

```json
{
  "page": {
    "name": "Facebook",
    "page_id": "100064860875397",
    "url": "https://www.facebook.com/facebook",
    "type": "page",
    "image": "https://scontent.xx.fbcdn.net/v/t39.30808-1/380700_..._n.jpg",
    "cover_image": "https://scontent.xx.fbcdn.net/v/t39.30808-6/513094_..._n.jpg",
    "followers": 155000000,
    "likes": null,
    "following": null,
    "categories": ["Page", "Internet company"],
    "intro": null,
    "website": "fb.me/HowToContactFB",
    "phone": null,
    "email": null,
    "address": null,
    "rating": null,
    "price_range": null,
    "verified": true,
    "delegate_page_id": "20531316728",
    "reels_page_id": "YXBwX2NvbGxlY3Rpb246cGZiaWQwcTlLYm..."
  }
}
```
