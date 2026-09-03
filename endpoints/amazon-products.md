# Amazon Product Search

Search Amazon products by keyword across 24 marketplaces. Returns ASIN, title, price, rating, Prime status, sales volume, and badges. Supports category, price, condition, brand, seller, deals, and rating filters.

## Endpoint

```
GET /v1/amazon/products
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword or a product ASIN (max 500 characters) |
| `page` | No | Page number, 1-20 (default: 1). Each page returns ~16 results |
| `country` | No | Marketplace country code (default: `us`). One of: `us`, `au`, `br`, `ca`, `cn`, `fr`, `de`, `in`, `it`, `mx`, `nl`, `sg`, `es`, `tr`, `ae`, `gb`, `jp`, `sa`, `pl`, `se`, `be`, `eg`, `za`, `ie` |
| `sort_by` | No | `relevance` (default), `lowest_price`, `highest_price`, `reviews`, `newest`, `best_sellers` |
| `category_id` | No | Category slug, e.g. `electronics`. See [Category IDs](/docs/amazon-categories) |
| `category` | No | Numeric Amazon category node ID(s) from an Amazon URL's `?node=` parameter. Comma-separated for multiple |
| `min_price` | No | Minimum price in the marketplace currency |
| `max_price` | No | Maximum price in the marketplace currency |
| `product_condition` | No | `all` (default), `new`, `used`, `renewed`, `collectible` |
| `brand` | No | Brand name(s), comma-separated for multiple |
| `seller_id` | No | Only products from specific seller ID(s), comma-separated |
| `is_prime` | No | Set to `true` to only return products with Prime-eligible offers |
| `deals_and_discounts` | No | `none` (default), `all_discounts`, `todays_deals` |
| `four_stars_and_up` | No | Set to `true` to only return products rated 4 stars and up |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `products` | array | Array of matching products |
| `products[].asin` | string | Amazon product ASIN — use in [Product Details](/docs/amazon-product-details) |
| `products[].title` | string | Product title |
| `products[].price` | string \| null | Current price with currency symbol (e.g. $299.99) |
| `products[].original_price` | string \| null | Pre-discount price when discounted |
| `products[].unit_price` | string \| null | Per-unit price when sold in multi-packs |
| `products[].unit_count` | integer \| null | Units per pack |
| `products[].currency` | string | Currency code (e.g. USD) |
| `products[].rating` | number \| null | Average star rating, 0.0-5.0 |
| `products[].num_ratings` | integer | Total ratings count |
| `products[].url` | string | Product page URL |
| `products[].photo` | string | Main product image URL |
| `products[].num_offers` | integer | Number of offers |
| `products[].minimum_offer_price` | string \| null | Lowest offer price |
| `products[].is_best_seller` | boolean | Has the Best Seller badge |
| `products[].is_amazon_choice` | boolean | Has the Amazon's Choice badge |
| `products[].is_prime` | boolean | Default offer is Prime |
| `products[].climate_pledge_friendly` | boolean | Has the Climate Pledge Friendly badge |
| `products[].sales_volume` | string \| null | Sales volume text (e.g. 5K+ bought in past month) |
| `products[].delivery` | string \| null | Delivery promise text |
| `products[].availability` | string \| null | Stock warning when low (e.g. Only 2 left in stock) |
| `products[].has_variations` | boolean | Product has variants (colors, sizes, etc.) |
| `products[].badge` | string \| null | Listing badge (e.g. Limited time deal) |
| `products[].coupon_text` | string \| null | Coupon text (e.g. Save 10% with coupon) |
| `total_products` | integer | Total matching products reported by Amazon |
| `query` | string | Echo of the search query |
| `page` | integer | Current page number |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/amazon/products?query=phone&sort_by=reviews&max_price=100" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/amazon/products",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "phone", "sort_by": "reviews", "max_price": 100}
)
print(response.json())
```

## Example Response

```json
{
  "products": [
    {
      "asin": "B0CTW8TXGH",
      "title": "Motorola Moto g Play 2024 | 64GB | 50MP Camera | Sapphire Blue",
      "price": "$39.88",
      "original_price": null,
      "unit_price": null,
      "unit_count": null,
      "currency": "USD",
      "rating": 4.3,
      "num_ratings": 856,
      "url": "https://www.amazon.com/dp/B0CTW8TXGH",
      "photo": "https://m.media-amazon.com/images/I/71fflP-3W4L._AC_UY654_FMwebp_QL65_.jpg",
      "num_offers": 1,
      "minimum_offer_price": "$39.88",
      "is_best_seller": false,
      "is_amazon_choice": true,
      "is_prime": true,
      "climate_pledge_friendly": false,
      "sales_volume": "5K+ bought in past month",
      "delivery": "FREE delivery Mon, Jun 9",
      "availability": null,
      "has_variations": false,
      "badge": "Overall Pick",
      "coupon_text": null
    }
  ],
  "count": 16,
  "total_products": 132661,
  "query": "phone",
  "page": 1
}
```

## Notes

- `country` selects the Amazon marketplace (e.g. `gb` searches amazon.co.uk); prices return in that marketplace's currency.
- `is_prime=true` filters to products with Prime-eligible offers; the `is_prime` field on each result reflects the default displayed offer's badge, which can differ.
