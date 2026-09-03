# Amazon Seller Profile

Get an Amazon seller's profile by seller ID: name, registered business details, average rating, and a feedback breakdown over 30 days, 90 days, 12 months, and lifetime.

## Endpoint

```
GET /v1/amazon/seller
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `seller_id` | Yes | Amazon seller ID (e.g. A2L77EE7U53NWQ), from a product's `main_buy_box.seller_id` or the `seller=` parameter of an Amazon seller URL |
| `country` | No | Marketplace country code (default: `us`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `seller` | object | Seller profile object |
| `seller.seller_id` | string | Seller ID |
| `seller.name` | string | Seller display name |
| `seller.seller_link` | string | Seller profile URL |
| `seller.store_link` | string \| null | Seller storefront URL |
| `seller.logo` | string \| null | Seller logo URL |
| `seller.about` | string \| null | About-this-seller text |
| `seller.business_name` | string \| null | Registered business name |
| `seller.business_address` | string \| null | Registered business address |
| `seller.rating` | number \| null | Average rating, 0.0-5.0 |
| `seller.ratings_total` | integer \| null | Total ratings count |
| `seller.positive_percentage` | integer \| null | Percentage of positive feedback |
| `seller.review_summary` | object | Feedback breakdown for `thirty_days`, `ninety_days`, `twelve_months`, `lifetime` — each with `positive_percent`, `neutral_percent`, `negative_percent`, `count` |
| `seller.country` | string | Marketplace country |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/amazon/seller?seller_id=A2L77EE7U53NWQ" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/amazon/seller",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"seller_id": "A2L77EE7U53NWQ"}
)
print(response.json())
```

## Example Response

```json
{
  "seller": {
    "seller_id": "A2L77EE7U53NWQ",
    "name": "Amazon Resale",
    "seller_link": "https://www.amazon.com/sp?seller=A2L77EE7U53NWQ",
    "store_link": "https://www.amazon.com/s?ie=UTF8&marketplaceID=ATVPDKIKX0DER&me=A2L77EE7U53NWQ",
    "logo": "https://m.media-amazon.com/images/I/01RxYGCdstL.gif",
    "about": "Quality used, pre-owned, or open box products, tested and inspected.",
    "business_name": "Amazon.com Services LLC",
    "business_address": "410 Terry Ave N Seattle WA 98109 US",
    "rating": 4.2,
    "ratings_total": 2593,
    "positive_percentage": 79,
    "review_summary": {
      "thirty_days": {"positive_percent": 75, "neutral_percent": 1, "negative_percent": 23, "count": 89},
      "ninety_days": {"positive_percent": 78, "neutral_percent": 1, "negative_percent": 21, "count": 232},
      "twelve_months": {"positive_percent": 79, "neutral_percent": 2, "negative_percent": 19, "count": 812},
      "lifetime": {"positive_percent": 82, "neutral_percent": 3, "negative_percent": 15, "count": 2593}
    },
    "country": "US"
  }
}
```

## Notes

- Sellers without public feedback stats (including some of Amazon's own storefronts) return `null` for `rating`, `ratings_total`, and `positive_percentage`.
