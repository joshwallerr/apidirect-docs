# Amazon Seller Reviews

Get customer feedback for an Amazon seller by seller ID. Each review includes author, text, star rating, date, and whether the seller responded. Filter by star rating or positive/critical sentiment.

## Endpoint

```
GET /v1/amazon/seller/reviews
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `seller_id` | Yes | Amazon seller ID |
| `page` | No | Page number, 1-50 (default: 1) |
| `star_rating` | No | `all` (default), `5_stars`, `4_stars`, `3_stars`, `2_stars`, `1_stars`, `positive`, `critical` |
| `country` | No | Marketplace country code (default: `us`) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (+$0.001/request) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `reviews` | array | Array of seller reviews |
| `reviews[].author_name` | string \| null | Reviewer display name |
| `reviews[].review_text` | string | Review body text |
| `reviews[].rating` | number \| null | Star rating, 1-5 |
| `reviews[].review_date` | string \| null | Review date (e.g. August 30, 2026) |
| `reviews[].has_response` | boolean | Whether the seller responded |
| `reviews[].sentiment` | object | Emotion analysis: emotions, dominant_emotion, emotional_intensity, polarity (when `get_sentiment=true`) |
| `seller_id` | string | Echo of the seller ID |
| `page` | integer | Current page number |
| `star_rating` | string | Echo of the star rating filter |
| `has_next_page` | boolean | Whether another page of reviews exists |
| `count` | integer | Number of reviews returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/amazon/seller/reviews?seller_id=A2L77EE7U53NWQ" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/amazon/seller/reviews",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"seller_id": "A2L77EE7U53NWQ"}
)
print(response.json())
```

## Example Response

```json
{
  "reviews": [
    {
      "author_name": "Tammy Parson",
      "review_text": "Received the next day in perfect condition. Contacted the seller and was answered promptly.",
      "rating": 5.0,
      "review_date": "August 30, 2026",
      "has_response": false
    }
  ],
  "count": 5,
  "seller_id": "A2L77EE7U53NWQ",
  "page": 1,
  "star_rating": "all",
  "has_next_page": true
}
```

## Notes

- `positive` returns 4-5 star feedback, `critical` returns 1-2 star feedback.
- Paginate with `page` until `has_next_page` is `false`.
