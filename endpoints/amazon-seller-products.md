# Amazon Seller Products

Get the catalog of products sold by an Amazon seller by seller ID. Returns the same product objects as [Product Search](/docs/amazon-products), plus the seller's total catalog size. Sortable and paginated.

## Endpoint

```
GET /v1/amazon/seller/products
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `seller_id` | Yes | Amazon seller ID |
| `page` | No | Page number, 1-20 (default: 1). Each page returns ~16 results |
| `sort_by` | No | `relevance` (default), `lowest_price`, `highest_price`, `reviews`, `newest`, `best_sellers` |
| `country` | No | Marketplace country code (default: `us`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `products` | array | The seller's products — same fields as [Product Search](/docs/amazon-products) items (`asin`, `title`, `price`, `rating`, `num_ratings`, `url`, `photo`, `is_prime`, `sales_volume`, etc.) |
| `total_products` | integer | Total products in the seller's catalog |
| `seller_id` | string | Echo of the seller ID |
| `page` | integer | Current page number |
| `sort_by` | string | Echoed sort order |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/amazon/seller/products?seller_id=A2L77EE7U53NWQ&sort_by=best_sellers" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/amazon/seller/products",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"seller_id": "A2L77EE7U53NWQ", "sort_by": "best_sellers"}
)
print(response.json())
```

## Example Response

```json
{
  "products": [
    {
      "asin": "B0BSHF7WHW",
      "title": "Apple AirPods Pro (2nd Generation) - Refurbished",
      "price": "$179.99",
      "original_price": "$249.00",
      "unit_price": null,
      "unit_count": null,
      "currency": "USD",
      "rating": 4.4,
      "num_ratings": 11203,
      "url": "https://www.amazon.com/dp/B0BSHF7WHW",
      "photo": "https://m.media-amazon.com/images/I/61SUj2aKoEL._AC_UY654_QL65_.jpg",
      "num_offers": 3,
      "minimum_offer_price": "$171.50",
      "is_best_seller": false,
      "is_amazon_choice": false,
      "is_prime": true,
      "climate_pledge_friendly": false,
      "sales_volume": "1K+ bought in past month",
      "delivery": "FREE delivery Tue, Sep 1",
      "availability": null,
      "has_variations": false,
      "badge": null,
      "coupon_text": null
    }
  ],
  "count": 16,
  "total_products": 224061,
  "seller_id": "A2L77EE7U53NWQ",
  "page": 1,
  "sort_by": "best_sellers"
}
```

## Notes

- Product objects are identical to Product Search items — the same parsing code works for both.
- Out-of-stock items can have a `null` price.
