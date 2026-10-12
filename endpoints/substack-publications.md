# Search Substack Publications

Search Substack publications by name or keyword. Returns name, URL, tagline, author, subscriber badge, paid-subscriber band, prices, bestseller tier and language for each publication.

## Endpoint

```
GET /v1/substack/publications
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `page` | No | Page number, 1-4 (default: 1). 20 publications per page |
| `language` | No | Two-letter language code, e.g. es, to rank publications in that language first |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `publications` | array | Array of matching publications |
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
| `publications[].subscriber_count_label` | string | The displayed subscriber badge, e.g. 1.2M+, or a band such as Thousands of subscribers |
| `publications[].ranking_detail` | string | Substack's ranking note: the paid-subscriber band for established publications or a launch note such as Launched a year ago for new ones; empty when not shown |
| `publications[].paid_subscriber_band` | string | Paid subscriber band, e.g. Tens of thousands of paid subscribers; empty when Substack shows none |
| `publications[].paid_subscriber_floor` | integer | Lower bound of the paid band (100, 1000, 10000), 0 when none |
| `publications[].bestseller_tier` | integer | Bestseller badge tier: 0, 100, 1000 or 10000 paid subscribers |
| `publications[].is_bestseller` | boolean | Whether the publication carries a bestseller badge |
| `publications[].paid_enabled` | boolean | Whether paid subscriptions are enabled |
| `publications[].plans` | array | Subscription prices (interval, amount, currency) |
| `publications[].has_podcast` | boolean | Whether the publication has a podcast |
| `publications[].podcast` | object/null | The publication's podcast (`title`, `description`, `art_url`, `host`, `is_free`, `is_subscriber_only`), null when none |
| `publications[].sections` | array | The publication's sections (`section_id`, `name`, `slug`, `is_podcast`) |
| `publications[].author_pic_url` | string | Primary author's profile picture URL |
| `publications[].logo_url_wide` | string | Wide logo URL, empty when none |
| `publications[].founding_plan_name` | string | Name of the founding tier, empty when none |
| `publications[].has_recommendations` | boolean | Whether the publication recommends other publications |
| `publications[].has_chat` | boolean | Whether subscriber chat is enabled |
| `publications[].language` | string | Language code |
| `publications[].type` | string | newsletter or podcast |
| `publications[].twitter_handle` | string | The publication's X handle, empty when none |
| `publications[].created_at` | string | Date the publication was created (UTC) |
| `publications[].first_post_date` | string | Date of the first post (UTC) |
| `publications[].source` | string | "Substack" |
| `publications[].domain` | string | "substack.com" |
| `query` | string | The search keyword |
| `page` | integer | Current page number |
| `has_next_page` | boolean | Whether another page exists |
| `count` | integer | Number of publications returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/publications?query=crypto&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/publications",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "crypto", "page": 1}
)
print(response.json())
```

## Example Response

```json
{
  "count": 20,
  "has_next_page": true,
  "page": 1,
  "publications": [
    {
      "author": "cryptoyall",
      "author_id": "89093778",
      "author_name": "Josh Rhodes - Crypto Y'all",
      "author_pic_url": "https://substackcdn.com/image/fetch/$s_!e6dX!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8ff3e27c-70ae-4556-9000-a84bf76e3dd3_2973x2377.jpeg",
      "author_url": "https://substack.com/@cryptoyall",
      "bestseller_tier": 0,
      "cover_image_url": "",
      "created_at": "2025-11-06 02:36:02",
      "custom_domain": "",
      "description": "Tired of feeling lost in the crypto world? We’ll teach you how the market really works—so you can spot opportunities, av…",
      "domain": "substack.com",
      "first_post_date": "2026-06-09 15:38:18",
      "founding_plan_name": "Founding Member",
      "has_chat": true,
      "has_podcast": true,
      "has_recommendations": false,
      "is_bestseller": false,
      "language": "en",
      "logo_url": "https://substackcdn.com/image/fetch/$s_!e6dX!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.…",
      "logo_url_wide": "https://substackcdn.com/image/fetch/$s_!3X7s!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F097d2cae-589f-466e-942c-e42391021862_480x254.png",
      "name": "Josh Rhodes - Crypto Y'all",
      "paid_enabled": true,
      "paid_subscriber_band": "",
      "paid_subscriber_floor": 0,
      "plans": [
        {
          "amount": 40.0,
          "currency": "USD",
          "interval": "month"
        },
        {
          "amount": 439.0,
          "currency": "USD",
          "interval": "year"
        }
      ],
      "podcast": null,
      "publication_id": "6822164",
      "ranking_detail": "Launched 4 months ago",
      "sections": [],
      "source": "Substack",
      "subdomain": "cryptoyall",
      "subscriber_count": null,
      "subscriber_count_label": "128",
      "twitter_handle": "",
      "type": "newsletter",
      "url": "https://cryptoyall.substack.com"
    }
  ],
  "query": "crypto"
}
```
