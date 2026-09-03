# Amazon Best Sellers

Get Amazon best-seller rankings for any category — Best Sellers, New Releases, Movers & Shakers, Most Wished For, or Gift Ideas. Each item includes rank, ASIN, title, price, and rating.

## Endpoint

```
GET /v1/amazon/best-sellers
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `category` | Yes | Category slug, e.g. `electronics` or `software`. See [Category IDs](/docs/amazon-categories) |
| `type` | No | `best_sellers` (default), `gift_ideas`, `most_wished_for`, `movers_and_shakers`, `new_releases` |
| `page` | No | Page number, 1 or 2 (default: 1). Each page returns up to 50 items; rankings cover the top 100 |
| `country` | No | Marketplace country code (default: `us`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `products` | array | Array of ranked products |
| `products[].rank` | integer | Position in the ranking |
| `products[].rank_change` | string \| null | Rank movement text (e.g. for Movers & Shakers) |
| `products[].asin` | string | Product ASIN |
| `products[].title` | string | Product title |
| `products[].price` | string \| null | Current price |
| `products[].rating` | number \| null | Average star rating, 0.0-5.0 |
| `products[].num_ratings` | integer | Total ratings count |
| `products[].url` | string | Product page URL |
| `products[].photo` | string | Product image URL |
| `category` | string | Echo of the requested category slug |
| `category_name` | string | Resolved category display name |
| `type` | string | Echo of the ranking type |
| `page` | integer | Current page number |
| `count` | integer | Number of items returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/amazon/best-sellers?category=software" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/amazon/best-sellers",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"category": "software"}
)
print(response.json())
```

## Example Response

```json
{
  "products": [
    {
      "rank": 1,
      "rank_change": null,
      "asin": "B0FWV56H48",
      "title": "TurboTax Deluxe Desktop Edition 2025, Federal & State Tax Return",
      "price": "$79.99",
      "rating": 4.0,
      "num_ratings": 6866,
      "url": "https://www.amazon.com/dp/B0FWV56H48",
      "photo": "https://images-na.ssl-images-amazon.com/images/I/71OcM906MLL._AC_UL900_SR900,600_.jpg"
    }
  ],
  "count": 50,
  "category": "software",
  "category_name": "Software",
  "type": "best_sellers",
  "page": 1
}
```

## Notes

- The five ranking types: `best_sellers` (top selling), `new_releases` (top selling new arrivals), `movers_and_shakers` (biggest 24h rank gainers), `most_wished_for` (most wish-listed), `gift_ideas` (most popular gifts).
- Rankings typically cover the top 100 items — pages 1-2 capture the full list.
- An unrecognized category slug returns an empty ranking rather than an error.
