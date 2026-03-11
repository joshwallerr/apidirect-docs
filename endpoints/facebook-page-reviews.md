# Facebook Page Reviews

Get reviews for a Facebook page by page ID. Returns review text, recommendation status, and author info. Supports fetching multiple pages in a single call.

## Endpoint

```
GET /v1/facebook/page/reviews
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `page_id` | Yes | Facebook page ID (get from page details or page ID endpoint) |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `reviews` | array | List of review objects |
| `reviews[].review_text` | string | Text content of the review |
| `reviews[].recommend` | boolean | Whether the reviewer recommends the page |
| `reviews[].author_name` | string | Name of the reviewer |
| `reviews[].author_url` | string | URL to the reviewer's profile |
| `reviews[].reactions_count` | integer | Number of reactions on the review |
| `count` | integer | Number of reviews returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/page/reviews?page_id=100063543614476" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/page/reviews",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"page_id": "100063543614476"}
)
print(response.json())
```

## Example Response

```json
{
  "reviews": [
    {
      "review_text": "Great customer service and fast response times. Highly recommend!",
      "recommend": true,
      "author_name": "Sarah Johnson",
      "author_url": "https://www.facebook.com/profile.php?id=100048392017456",
      "reactions_count": 12
    },
    {
      "review_text": "Decent product but shipping took longer than expected.",
      "recommend": true,
      "author_name": "Michael Chen",
      "author_url": "https://www.facebook.com/profile.php?id=100039284710385",
      "reactions_count": 4
    }
  ],
  "count": 2,
  "pages": 1
}
```
