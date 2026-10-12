# Substack Category Publications

Get a Substack category's leaderboard: the top publications ranked by Substack, each with its full details (subscriber badge, paid band, prices, author) and rank.

## Endpoint

```
GET /v1/substack/category/publications
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `category` | Yes | Category ID (e.g. `4`) or slug (e.g. `technology`), or `bestsellers` / `podcasts` for the site-wide boards. See [Category IDs](/docs/substack-category-ids) |
| `tier` | No | `all`, `paid` or `rising` (default: `all`). `bestsellers` has `rising` only; `podcasts` has `all` and `paid` |
| `page` | No | Page number (default: 1), 25 publications per page. Up to 21 pages; rising 10; bestsellers and podcasts 4 |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `publications` | array | Ranked publications |
| `publications[].rank` | integer | Position on the board |
| `publications[].publication_id` | string | Publication ID |
| `publications[].name` | string | Publication name |
| `publications[].subdomain` | string | Substack subdomain (`<subdomain>.substack.com`) |
| `publications[].url` | string | Publication home URL (the custom domain when it has one) |
| `publications[].custom_domain` | string | Custom domain, empty when none |
| `publications[].description` | string | Publication tagline |
| `publications[].logo_url` | string | Logo URL |
| `publications[].cover_image_url` | string | Cover image URL, empty when none |
| `publications[].author` | string | Primary author's handle |
| `publications[].author_name` | string | Primary author's display name |
| `publications[].author_id` | string | Primary author's user ID |
| `publications[].author_url` | string | Link to the primary author's profile |
| `publications[].subscriber_count` | integer/null | Free subscriber count as Substack displays it (rounded, e.g. 1200000); null when the publication hides it |
| `publications[].subscriber_count_label` | string | The displayed subscriber badge, e.g. `1.2M+`, or a band such as `Thousands of subscribers` |
| `publications[].ranking_detail` | string | Substack's ranking note: the paid-subscriber band for established publications or a launch note such as `Launched a year ago` for new ones; empty when not shown |
| `publications[].paid_subscriber_band` | string | Paid subscriber band, e.g. `Tens of thousands of paid subscribers`; empty when Substack shows none |
| `publications[].paid_subscriber_floor` | integer | Lower bound of the paid band (100, 1000, 10000), 0 when none |
| `publications[].bestseller_tier` | integer | Bestseller badge tier: 0, 100, 1000 or 10000 paid subscribers |
| `publications[].is_bestseller` | boolean | Whether the publication carries a bestseller badge |
| `publications[].paid_enabled` | boolean | Whether paid subscriptions are enabled |
| `publications[].plans` | array | Subscription prices (`interval`, `amount`, `currency`) |
| `publications[].has_podcast` | boolean | Whether the publication has a podcast |
| `publications[].podcast` | object/null | The publication's podcast (`title`, `description`, `art_url`, `host`, `is_free`, `is_subscriber_only`), null when none |
| `publications[].sections` | array | The publication's sections (`section_id`, `name`, `slug`, `is_podcast`) |
| `publications[].author_pic_url` | string | Primary author's profile picture URL |
| `publications[].logo_url_wide` | string | Wide logo URL, empty when none |
| `publications[].founding_plan_name` | string | Name of the founding tier, empty when none |
| `publications[].has_recommendations` | boolean | Whether the publication recommends other publications |
| `publications[].has_chat` | boolean | Whether subscriber chat is enabled |
| `publications[].language` | string | Language code |
| `publications[].type` | string | `newsletter` or `podcast` |
| `publications[].twitter_handle` | string | The publication's X handle, empty when none |
| `publications[].created_at` | string | Date the publication was created (UTC) |
| `publications[].first_post_date` | string | Date of the first post (UTC) |
| `publications[].source` | string | `"Substack"` |
| `publications[].domain` | string | `"substack.com"` |
| `category` | object | The category (`category_id`, `name`) |
| `tier` | string | The board requested |
| `page` | integer | Current page number |
| `has_next_page` | boolean | Whether another page exists |
| `count` | integer | Number of publications returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/category/publications?category=technology&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/category/publications",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"category": "technology", "page": 1}
)
print(response.json())
```

## Example Response

```json
{
  "category": {
    "category_id": 4,
    "name": "Technology"
  },
  "count": 25,
  "has_next_page": true,
  "page": 1,
  "publications": [
    {
      "author": "bytebytego",
      "author_id": "22329494",
      "author_name": "Alex Xu",
      "author_pic_url": "",
      "author_url": "https://substack.com/@bytebytego",
      "bestseller_tier": 0,
      "cover_image_url": "https://substack-post-media.s3.amazonaws.com/public/images/a4e1c1bd-03ee-4126-b3e4-19553b2d2fc6_1279x821.png",
      "created_at": "2022-03-27 03:36:45",
      "custom_domain": "blog.bytebytego.com",
      "description": "Explain complex systems with simple terms, from the authors of the best-selling system design book series. Join over 1,000,000 friendly readers.",
      "domain": "substack.com",
      "first_post_date": "2021-11-25 17:31:00",
      "founding_plan_name": "",
      "has_chat": false,
      "has_podcast": false,
      "has_recommendations": false,
      "is_bestseller": false,
      "language": "en",
      "logo_url": "https://substackcdn.com/image/fetch/$s_!1eXV!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazona…",
      "logo_url_wide": "",
      "name": "ByteByteGo Newsletter",
      "paid_enabled": true,
      "paid_subscriber_band": "",
      "paid_subscriber_floor": 0,
      "plans": [
        {
          "amount": 15.0,
          "currency": "USD",
          "interval": "month"
        }
      ],
      "podcast": null,
      "publication_id": "817132",
      "rank": 1,
      "ranking_detail": "",
      "sections": [],
      "source": "Substack",
      "subdomain": "bytebytego",
      "subscriber_count": null,
      "subscriber_count_label": "",
      "twitter_handle": "alexxubyte",
      "type": "newsletter",
      "url": "https://blog.bytebytego.com"
    }
  ],
  "tier": "all"
}
```
