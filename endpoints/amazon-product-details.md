# Amazon Product Details

Get full details for an Amazon product by ASIN: pricing, buy box (with seller ID), availability, photos, specs, rating breakdown, and top reviews.

## Endpoint

```
GET /v1/amazon/product
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `asin` | Yes | 10-character Amazon ASIN (e.g. B07ZPKN6YR), as returned by [Product Search](/docs/amazon-products) |
| `country` | No | Marketplace country code (default: `us`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `product` | object | Full product object |
| `product.asin` | string | Product ASIN |
| `product.title` | string | Product title |
| `product.item_highlight` | string \| null | Short highlight line |
| `product.price` | string \| null | Current price |
| `product.original_price` | string \| null | Pre-discount price |
| `product.delivery_price` | string \| null | Delivery price text |
| `product.minimum_order_quantity` | integer \| null | Minimum order quantity |
| `product.currency` | string | Currency code |
| `product.country` | string | Marketplace country |
| `product.byline` | string \| null | Byline text (e.g. Visit the Apple Store) |
| `product.byline_link` | string \| null | Byline URL (brand / store page) |
| `product.rating` | number \| null | Average star rating, 0.0-5.0 |
| `product.num_ratings` | integer | Total ratings count |
| `product.url` | string | Product page URL |
| `product.slug` | string \| null | Product URL slug |
| `product.photo` | string | Main image URL |
| `product.photos` | array | All product image URLs |
| `product.videos` | array | Product video objects |
| `product.user_uploaded_videos` | array | Customer-uploaded video objects |
| `product.has_video` | boolean | Product page has video |
| `product.num_offers` | integer | Number of offers |
| `product.availability` | string \| null | Availability text (e.g. In Stock) |
| `product.condition` | string \| null | Buy box condition (e.g. Buy New) |
| `product.is_best_seller` | boolean | Has the Best Seller badge |
| `product.is_amazon_choice` | boolean | Has the Amazon's Choice badge |
| `product.is_prime` | boolean | Prime-eligible |
| `product.climate_pledge_friendly` | boolean | Has the Climate Pledge Friendly badge |
| `product.sales_volume` | string \| null | Sales volume text |
| `product.delivery` | string \| null | Delivery promise text |
| `product.main_buy_box` | object \| null | Winning offer: `title`, `price`, `seller`, `seller_id`, `seller_link`, `return_policy` |
| `product.buy_boxes` | array | All buy boxes (e.g. Buy New / Buy Used), same shape as `main_buy_box` |
| `product.about` | array | About This Item bullet points |
| `product.description` | string \| null | Product description text |
| `product.product_information` | object | Product Information table as key-value pairs |
| `product.product_details` | object | Product overview attributes (Brand, Model, etc.) |
| `product.rating_distribution` | object | Percentage of ratings per star (keys 1-5) |
| `product.top_reviews` | array | Top reviews from the product page (see below) |
| `product.top_reviews[].review_id` | string | Review identifier |
| `product.top_reviews[].title` | string \| null | Review title |
| `product.top_reviews[].review_text` | string | Review body text |
| `product.top_reviews[].rating` | number \| null | Star rating, 1-5 |
| `product.top_reviews[].review_link` | string \| null | Direct review URL |
| `product.top_reviews[].review_date` | string \| null | Review date text |
| `product.top_reviews[].author_id` | string \| null | Reviewer account ID |
| `product.top_reviews[].author_name` | string \| null | Reviewer display name |
| `product.top_reviews[].author_avatar` | string \| null | Reviewer avatar URL |
| `product.top_reviews[].images` | array | Photo URLs attached to the review |
| `product.top_reviews[].video` | object \| null | Video attached to the review |
| `product.top_reviews[].is_verified_purchase` | boolean | Verified purchase |
| `product.top_reviews[].helpful_votes` | string \| null | Helpful votes text (e.g. 12 people found this helpful) |
| `product.top_reviews[].product_variant` | object | Reviewed variant (e.g. Size, Color) |
| `product.top_reviews[].is_vine` | boolean | Vine program review |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/amazon/product?asin=B07ZPKN6YR" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/amazon/product",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"asin": "B07ZPKN6YR"}
)
print(response.json())
```

## Example Response

```json
{
  "product": {
    "asin": "B07ZPKN6YR",
    "title": "Apple iPhone 11, 64GB, Black - Unlocked (Renewed)",
    "item_highlight": "Fully unlocked, renewed and inspected, 64GB storage",
    "price": "$190.00",
    "original_price": "$249.00",
    "delivery_price": null,
    "minimum_order_quantity": null,
    "currency": "USD",
    "country": "US",
    "byline": "Visit the Amazon Renewed Store",
    "byline_link": "https://www.amazon.com/Amazon-Renewed/b/...",
    "rating": 4.2,
    "num_ratings": 57539,
    "url": "https://www.amazon.com/dp/B07ZPKN6YR",
    "slug": "Apple-iPhone-11-64GB-Black",
    "photo": "https://m.media-amazon.com/images/I/514k7uOBMwL._AC_SL1000_.jpg",
    "photos": ["https://m.media-amazon.com/images/I/514k7uOBMwL._AC_SL1000_.jpg"],
    "videos": [],
    "user_uploaded_videos": [],
    "has_video": false,
    "num_offers": 47,
    "availability": "In Stock",
    "condition": "Buy New",
    "is_best_seller": false,
    "is_amazon_choice": false,
    "is_prime": false,
    "climate_pledge_friendly": false,
    "sales_volume": "2K+ bought in past month",
    "delivery": "FREE delivery Friday, June 6",
    "main_buy_box": {
      "title": "Buy New",
      "price": "$190.00",
      "seller": "iBlueberry",
      "seller_id": "A1B2C3D4E5F6G7",
      "seller_link": "https://www.amazon.com/gp/help/seller/at-a-glance.html/...",
      "return_policy": "30-day refund/replacement"
    },
    "buy_boxes": [{"title": "Buy New", "price": "$190.00"}],
    "about": ["This phone is unlocked and compatible with any carrier of choice."],
    "description": "The iPhone 11 features a 6.1-inch Liquid Retina display...",
    "product_information": {"Screen Size": "6.1 inches", "Color": "Black"},
    "product_details": {"Brand": "Apple", "Model Name": "iPhone 11"},
    "rating_distribution": {"1": "12", "2": "3", "3": "5", "4": "12", "5": "68"},
    "top_reviews": [
      {
        "review_id": "R3PXA2ZA1TUMCE",
        "title": "Five stars !! It's worth the money !!",
        "review_text": "I had my phone for a couple of years... it was a perfect phone.",
        "rating": 5.0,
        "review_link": "https://www.amazon.com/gp/customer-reviews/R3PXA2ZA1TUMCE",
        "review_date": "Reviewed in the United States on October 30, 2025",
        "author_id": "AHDG3DAH75Y6DILGMFNKDAXGX7YQ",
        "author_name": "Dorothyann",
        "author_avatar": "https://m.media-amazon.com/images/S/amazon-avatars-global/default.png",
        "images": [],
        "video": null,
        "is_verified_purchase": true,
        "helpful_votes": "12 people found this helpful",
        "product_variant": {"Size": "64GB", "Color": "Purple"},
        "is_vine": false
      }
    ]
  }
}
```

## Notes

- One ASIN per request. For bulk lookups, use [/v1/batch](/docs/batch) — up to 100 lookups in one call.
- `main_buy_box.seller_id` identifies who sells the product — pass it to [Seller Profile](/docs/amazon-seller-profile), [Seller Reviews](/docs/amazon-seller-reviews), or [Seller Products](/docs/amazon-seller-products).
