# Substack Publication Details

Get a Substack publication by subdomain, custom domain, URL or ID. Returns name, tagline, logo, author, the subscriber badge and paid-subscriber band Substack displays, bestseller tier, subscription prices, podcast flag, language, launch dates and the publication's contributors.

## Endpoint

```
GET /v1/substack/publication
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

Provide exactly one of `publication` or `publication_id`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `publication` | One required | Publication subdomain (`lenny`), host (`lenny.substack.com`, `www.lennysnewsletter.com`) or any URL on it (max 500 characters). Provide either `publication` or `publication_id`. |
| `publication_id` | One required | Numeric publication ID, as returned in `publication_id`. Provide either `publication` or `publication_id`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `publication` | object | Publication data |
| `publication.publication_id` | string | Publication ID |
| `publication.name` | string | Publication name |
| `publication.subdomain` | string | Substack subdomain (`<subdomain>.substack.com`) |
| `publication.url` | string | Publication home URL (the custom domain when it has one) |
| `publication.custom_domain` | string | Custom domain, empty when none |
| `publication.description` | string | Publication tagline |
| `publication.logo_url` | string | Logo URL |
| `publication.cover_image_url` | string | Cover image URL, empty when none |
| `publication.author` | string | Primary author's handle |
| `publication.author_name` | string | Primary author's display name |
| `publication.author_id` | string | Primary author's user ID |
| `publication.author_url` | string | Link to the primary author's profile |
| `publication.subscriber_count` | integer/null | Free subscriber count as Substack displays it (rounded, e.g. 1200000); null when the publication hides it |
| `publication.subscriber_count_label` | string | The displayed subscriber badge, e.g. `1.2M+`, or a band such as `Thousands of subscribers` |
| `publication.ranking_detail` | string | Substack's ranking note: the paid-subscriber band for established publications or a launch note such as `Launched a year ago` for new ones; empty when not shown |
| `publication.paid_subscriber_band` | string | Paid subscriber band, e.g. `Tens of thousands of paid subscribers`; empty when Substack shows none |
| `publication.paid_subscriber_floor` | integer | Lower bound of the paid band (100, 1000, 10000), 0 when none |
| `publication.bestseller_tier` | integer | Bestseller badge tier: 0, 100, 1000 or 10000 paid subscribers |
| `publication.is_bestseller` | boolean | Whether the publication carries a bestseller badge |
| `publication.paid_enabled` | boolean | Whether paid subscriptions are enabled |
| `publication.plans` | array | Subscription prices (`interval`, `amount`, `currency`) |
| `publication.has_podcast` | boolean | Whether the publication has a podcast |
| `publication.podcast` | object/null | The publication's podcast (`title`, `description`, `art_url`, `host`, `is_free`, `is_subscriber_only`), null when none |
| `publication.sections` | array | The publication's sections (`section_id`, `name`, `slug`, `is_podcast`) |
| `publication.author_pic_url` | string | Primary author's profile picture URL |
| `publication.logo_url_wide` | string | Wide logo URL, empty when none |
| `publication.founding_plan_name` | string | Name of the founding tier, empty when none |
| `publication.has_recommendations` | boolean | Whether the publication recommends other publications |
| `publication.has_chat` | boolean | Whether subscriber chat is enabled |
| `publication.language` | string | Language code |
| `publication.type` | string | `newsletter` or `podcast` |
| `publication.twitter_handle` | string | The publication's X handle, empty when none |
| `publication.created_at` | string | Date the publication was created (UTC) |
| `publication.first_post_date` | string | Date of the first post (UTC) |
| `publication.source` | string | `"Substack"` |
| `publication.domain` | string | `"substack.com"` |
| `publication.contributors` | array | People who write for the publication |
| `publication.contributors[].username` | string | Contributor's handle |
| `publication.contributors[].full_name` | string | Display name |
| `publication.contributors[].user_id` | string | User ID |
| `publication.contributors[].biography` | string | Bio |
| `publication.contributors[].profile_pic_url` | string | Profile picture URL |
| `publication.contributors[].bestseller_tier` | integer | Bestseller badge tier, 0 when none |
| `publication.contributors[].is_byline_only` | boolean | Whether the person only appears in bylines rather than as a publication member |
| `publication.contributors[].url` | string | Link to the profile |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/publication?publication=lenny" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/publication",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"publication": "lenny"}
)
print(response.json())
```

## Example Response

```json
{
  "publication": {
    "author": "lenny",
    "author_id": "1849774",
    "author_name": "Lenny Rachitsky",
    "author_pic_url": "",
    "author_url": "https://substack.com/@lenny",
    "bestseller_tier": 10000,
    "contributors": [
      {
        "bestseller_tier": 0,
        "biography": "Student of products. I write to learn, share and meet kindred spirits ✨.  ",
        "full_name": "Kiyani",
        "is_byline_only": false,
        "profile_pic_url": "https://bucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com/public/images/48e9d3e5-91eb-41be-9701-420b01f6585f_313x321.jpeg",
        "url": "https://substack.com/@kiyani",
        "user_id": "3667529",
        "username": "kiyani"
      }
    ],
    "cover_image_url": "https://substack-post-media.s3.amazonaws.com/public/images/4a25905e-c484-4885-80fa-9c2e683e362b_592x592.png",
    "created_at": "2019-06-01 15:35:37",
    "custom_domain": "www.lennysnewsletter.com",
    "description": "Deeply researched product, growth, and career advice for product leaders, founders, and ambitious builders.\n",
    "domain": "substack.com",
    "first_post_date": "2019-06-14 15:00:48",
    "founding_plan_name": "",
    "has_chat": false,
    "has_podcast": true,
    "has_recommendations": false,
    "is_bestseller": true,
    "language": "en",
    "logo_url": "https://substackcdn.com/image/fetch/$s_!8MSN!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F…",
    "logo_url_wide": "",
    "name": "Lenny's Newsletter",
    "paid_enabled": true,
    "paid_subscriber_band": "Tens of thousands of paid subscribers",
    "paid_subscriber_floor": 10000,
    "plans": [
      {
        "amount": 20.0,
        "currency": "USD",
        "interval": "month"
      }
    ],
    "podcast": null,
    "publication_id": "10845",
    "ranking_detail": "Tens of thousands of paid subscribers",
    "sections": [],
    "source": "Substack",
    "subdomain": "lenny",
    "subscriber_count": 1200000,
    "subscriber_count_label": "1.2M+",
    "twitter_handle": "lennysan",
    "type": "newsletter",
    "url": "https://www.lennysnewsletter.com"
  }
}
```
