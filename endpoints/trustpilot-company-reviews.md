# Trustpilot Company Reviews

Get a company's Trustpilot reviews and full profile by website domain. Each page returns up to 20 reviews; one call fetches up to 10 pages.

## Endpoint

```
GET /v1/trustpilot/company/reviews
```

**Price:** $0.005 per page
**Free tier:** 50 requests/month

Each page returns up to 20 reviews.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `domain` | Yes | Company website domain (e.g. gossby.com) or its Trustpilot review-page URL (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1). Each page returns up to 20 reviews and is billed as one request |
| `sort_by` | No | most_relevant (default), newest |
| `rating` | No | Only reviews with these star ratings, comma-separated 1-5 (e.g. 1,2 or 5) |
| `posted_ago` | No | Only reviews from this period: 30d, 3m, 6m, 12m (default: all time) |
| `language` | No | 2-letter ISO 639-1 language code (e.g. en, de). Default: all languages |
| `verified` | No | Set to true to return only verified reviews |
| `with_replies` | No | Set to true to return only reviews the company has replied to |
| `query` | No | Only reviews matching this keyword or phrase (max 500 characters) |
| `get_sentiment` | No | Set to true to add AI emotion analysis (+$0.001/page) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `company` | object | The company's full Trustpilot profile |
| `company.business_unit_id` | string | Trustpilot business unit ID |
| `company.name` | string | Company display name |
| `company.domain` | string | Company website domain |
| `company.website` | string \| null | Company website URL |
| `company.url` | string | Trustpilot review page URL |
| `company.logo` | string \| null | Company logo URL |
| `company.rating` | number \| null | TrustScore, 1.0-5.0 (Trustpilot's weighted score, favours recent reviews) |
| `company.stars` | number \| null | TrustScore rounded to the nearest half star (display value) |
| `company.review_count` | integer \| null | Total number of reviews |
| `company.review_count_last_12_months` | integer \| null | Reviews posted in the last 12 months |
| `company.reviews_per_rating` | object | Count of reviews per star (`{"1": N, "2": N, ... "5": N}`) |
| `company.categories` | array | Category names the company is listed in (strings) |
| `company.category_path` | array | Breadcrumb from the top-level category down to the primary category |
| `company.is_claimed` | boolean | Whether the business has claimed its Trustpilot profile |
| `company.claimed_date` | string \| null | ISO 8601 datetime the profile was claimed |
| `company.is_closed` | boolean | Whether the business is marked closed |
| `company.is_temporarily_closed` | boolean | Whether the business is marked temporarily closed |
| `company.is_collecting_reviews` | boolean | Whether the business is actively collecting reviews through Trustpilot |
| `company.verification` | object | Business verification flags: `verified_payment_method`, `verified_user_identity`, `verified_by_google` |
| `company.reply_behavior` | object | How the business replies: `reply_percentage`, `average_days_to_reply`, `negative_reviews_with_replies`, `total_negative_reviews`, `last_reply_to_negative` |
| `company.email` | string \| null | Contact email |
| `company.phone_number` | string \| null | Contact phone number (as listed, not normalized) |
| `company.address` | string \| null | Street address |
| `company.city` | string \| null | City |
| `company.zipcode` | string \| null | Postal code |
| `company.country` | string \| null | 2-letter ISO 3166-1 country code |
| `company.locations_count` | integer \| null | Number of business locations listed |
| `company.topics` | array | Topics customers mention most (strings, e.g. `Delivery service`) |
| `reviews` | array | Array of reviews, newest or most relevant first |
| `reviews[].review_id` | string | Trustpilot review ID |
| `reviews[].review_link` | string | Direct link to the review on Trustpilot |
| `reviews[].rating` | integer | Star rating, 1-5 |
| `reviews[].title` | string \| null | Review title |
| `reviews[].review_text` | string | Review body text |
| `reviews[].review_language` | string \| null | Review language code (e.g. `en`) |
| `reviews[].review_datetime_utc` | string | ISO 8601 datetime the review was published (UTC) |
| `reviews[].review_timestamp` | integer | Unix timestamp (seconds) of publication |
| `reviews[].experience_date` | string \| null | Date of the experience the review describes (`YYYY-MM-DD`) |
| `reviews[].updated_datetime_utc` | string \| null | ISO 8601 datetime of the last edit, or `null` |
| `reviews[].is_verified` | boolean | Whether the review is verified |
| `reviews[].verification_level` | string | `verified`, `invited` (the company invited the reviewer) or `not-verified` |
| `reviews[].like_count` | integer | Number of "useful" votes |
| `reviews[].author_id` | string | Reviewer ID — pass to [User Profile](/docs/trustpilot-user) as `user_id` |
| `reviews[].author_name` | string \| null | Reviewer display name |
| `reviews[].author_country` | string \| null | Reviewer's 2-letter country code |
| `reviews[].author_review_count` | integer \| null | Total reviews the reviewer has written |
| `reviews[].author_link` | string | Reviewer profile URL |
| `reviews[].owner_response` | object \| null | Object with `text`, `datetime_utc`, `timestamp` when the company has replied |
| `reviews[].sentiment` | object | Emotion analysis: `emotions`, `dominant_emotion`, `emotional_intensity`, `polarity` (when `get_sentiment=true`) |
| `count` | integer | Number of reviews returned |
| `pages` | integer | Echo of requested pages |
| `sort_by` | string | Echoed sort order |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/trustpilot/company/reviews?domain=gossby.com&pages=2&sort_by=newest" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/trustpilot/company/reviews",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "domain": "gossby.com",
        "pages": 2,
        "sort_by": "newest"
    }
)
print(response.json())
```

## Example Response

```json
{
  "company": {
    "business_unit_id": "5dc962f10fdaf000012b2f08",
    "name": "Gossby",
    "domain": "gossby.com",
    "website": "https://gossby.com",
    "url": "https://www.trustpilot.com/review/gossby.com",
    "logo": "https://s3-eu-west-1.amazonaws.com/tpd/logos/5dc962f10fdaf000012b2f08/0x0.png",
    "rating": 4.2,
    "stars": 4.0,
    "review_count": 37687,
    "review_count_last_12_months": 1313,
    "reviews_per_rating": {
      "1": 3934,
      "2": 1110,
      "3": 1516,
      "4": 2829,
      "5": 28298
    },
    "categories": [
      "Gift Shop",
      "Clothing Store",
      "Hobby Store"
    ],
    "category_path": [
      "Shopping & Fashion",
      "Clothing & Underwear",
      "Clothing Store"
    ],
    "is_claimed": true,
    "claimed_date": "2019-11-15T04:26:53.000Z",
    "is_closed": false,
    "is_temporarily_closed": false,
    "is_collecting_reviews": false,
    "verification": {
      "verified_payment_method": false,
      "verified_user_identity": true,
      "verified_by_google": true
    },
    "reply_behavior": {
      "reply_percentage": 98.7012987012987,
      "average_days_to_reply": 0.25,
      "negative_reviews_with_replies": 228,
      "total_negative_reviews": 231,
      "last_reply_to_negative": "2026-09-06 01:30:03 UTC"
    },
    "email": "support@gossby.com",
    "phone_number": "(585) 366 8846",
    "address": "6901 Riverport Dr",
    "city": "Louisville",
    "zipcode": "40258",
    "country": "US",
    "locations_count": 0,
    "topics": [
      "Order",
      "Delivery service",
      "Product",
      "Quality",
      "Christmas",
      "Customer service",
      "Service",
      "Customer communications",
      "Price",
      "Location",
      "Website",
      "Recommendation",
      "Mistake",
      "Solution",
      "Marketing"
    ]
  },
  "reviews": [
    {
      "review_id": "6a9e02811b7c1d51f71113ca",
      "review_link": "https://www.trustpilot.com/reviews/6a9e02811b7c1d51f71113ca",
      "rating": 5,
      "title": "5 stars all around",
      "review_text": "There are lots of great products. I had trouble narrowing it down. I like the preview option to see what the personalization would look like. The product was delivered faster than I expected and looked great. I’ll be back.",
      "review_language": "en",
      "review_datetime_utc": "2026-09-07T02:17:05.000Z",
      "review_timestamp": 1788747425,
      "experience_date": "2026-09-06",
      "updated_datetime_utc": null,
      "is_verified": false,
      "verification_level": "not-verified",
      "like_count": 0,
      "author_id": "6a9e0193452b16209f5549a1",
      "author_name": "Ash",
      "author_country": "US",
      "author_review_count": 1,
      "author_link": "https://www.trustpilot.com/users/6a9e0193452b16209f5549a1",
      "owner_response": null
    },
    {
      "review_id": "6a9db9402386d1ebd2295f29",
      "review_link": "https://www.trustpilot.com/reviews/6a9db9402386d1ebd2295f29",
      "rating": 5,
      "title": "I love the You and Me & the Dog mug",
      "review_text": "I love the You and Me & the Dog mug. The amount of design options is great, nice colors and sizes. The only problem I had was when I ordered blue trim I didn’t realize it only came in the smaller size mug. Something to be aware of.",
      "review_language": "en",
      "review_datetime_utc": "2026-09-06T21:04:32.000Z",
      "review_timestamp": 1788728672,
      "experience_date": "2026-09-06",
      "updated_datetime_utc": null,
      "is_verified": false,
      "verification_level": "invited",
      "like_count": 0,
      "author_id": "5693f8c70000ff0001fb4ce3",
      "author_name": "Darleen",
      "author_country": "US",
      "author_review_count": 5,
      "author_link": "https://www.trustpilot.com/users/5693f8c70000ff0001fb4ce3",
      "owner_response": null
    }
  ],
  "count": 2,
  "pages": 2,
  "sort_by": "newest"
}
```

## Notes

- Trustpilot serves at most 200 reviews per view (10 pages of 20). Combine `sort_by`, `rating`, `posted_ago`, `language` and `query` to reach different slices of a large company's reviews.
- `company.rating` is the TrustScore, a weighted score that favours recent reviews; it is not the arithmetic mean of `reviews_per_rating`. `stars` is the TrustScore rounded to the nearest half for display.
- `verification_level` is `invited` when the company asked the customer for a review; `is_verified` is `true` only for `verified`.
- `language` is a Trustpilot filter and is approximate — an occasional review in another language can appear.
