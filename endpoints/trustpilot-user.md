# Trustpilot User Profile

Get a Trustpilot reviewer's public profile and the reviews they have written across all companies, 20 per page.

## Endpoint

```
GET /v1/trustpilot/user
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

Each page returns up to 20 reviews.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `user_id` | Yes | Reviewer ID (24 hex characters), from a review's author_id on [Company Reviews](/docs/trustpilot-company-reviews). A trustpilot.com/users/... URL also works |
| `page` | No | Page number, 1-500 (default: 1). Each page returns up to 20 reviews |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `user` | object | Reviewer profile |
| `user.user_id` | string | Reviewer ID |
| `user.name` | string \| null | Display name |
| `user.country` | string \| null | Country name |
| `user.review_count` | integer \| null | Total reviews written |
| `user.verified` | boolean | Whether the reviewer's identity is verified |
| `user.has_product_reviews` | boolean | Whether the reviewer has written product reviews |
| `user.likes` | integer \| null | Total "useful" votes received |
| `user.reads` | integer \| null | Total times their reviews were read |
| `user.url` | string | Reviewer profile URL |
| `reviews` | array | Reviews written by the user, newest first |
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
| `reviews[].company_name` | string \| null | Reviewed company name |
| `reviews[].company_domain` | string \| null | Reviewed company domain — pass to [Company Reviews](/docs/trustpilot-company-reviews) |
| `reviews[].company_url` | string \| null | Reviewed company's Trustpilot page URL |
| `reviews[].business_unit_id` | string \| null | Reviewed company's business unit ID |
| `reviews[].owner_response` | object \| null | Object with `text`, `datetime_utc`, `timestamp` when the company has replied |
| `count` | integer | Number of reviews returned |
| `page` | integer | Current page number |
| `total_pages` | integer \| null | Total pages of reviews |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/trustpilot/user?user_id=5724f5f50000ff000a1c0f61" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/trustpilot/user",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"user_id": "5724f5f50000ff000a1c0f61"}
)
print(response.json())
```

## Example Response

```json
{
  "user": {
    "user_id": "5724f5f50000ff000a1c0f61",
    "name": "Phillip Williams.",
    "country": "United Kingdom",
    "review_count": 134,
    "verified": true,
    "has_product_reviews": false,
    "likes": 136,
    "reads": 19656,
    "url": "https://www.trustpilot.com/users/5724f5f50000ff000a1c0f61"
  },
  "reviews": [
    {
      "review_id": "6a9ddb3f9185b6cc96d8b88f",
      "review_link": "https://www.trustpilot.com/reviews/6a9ddb3f9185b6cc96d8b88f",
      "rating": 1,
      "title": "Please just fix my landline.",
      "review_text": "Just had my broadband upgraded. Nice.\nUnfortunately my land line is now dead, mort, kapoot, silent, no more.\nWould you please arrange to fix it.\nI did try calling last friday, only to be told waiting times were in excess of 30 minutes.\nI'm not sitting on the phone twiddling my b****cks for 30 minutes waiting for you to answer the phone.\nPlease arrange to have my landline fixed, and I promise not to leave you a one star review (every day) until you do.\nI will of course remove this review once you have fixed my land line.\nAccount 3225076\n\nJust tried calling again, only to be told current waiting time is over half and hour.",
      "review_language": "en",
      "review_datetime_utc": "2026-09-06T23:29:35.000Z",
      "review_timestamp": 1788737375,
      "experience_date": "2026-09-06",
      "updated_datetime_utc": "2026-09-07T13:26:39.000Z",
      "is_verified": false,
      "verification_level": "not-verified",
      "like_count": 0,
      "company_name": "Utility Warehouse",
      "company_domain": "uw.co.uk",
      "company_url": "https://www.trustpilot.com/review/uw.co.uk",
      "business_unit_id": "48e8f676000064000503c337",
      "owner_response": {
        "text": "Hi Phillip,\n\nWe are very sorry to hear that your landline is non functional following your broadband upgrade and that you experienced such a long wait time when calling us.\n\nWe are unable to fix the landline via this platform, so you will need to call our Technical team on 0333 777 0777 so they can access your account details and resolve this for you.\n\nThanks,\nThe Utility Warehouse Team",
        "datetime_utc": "2026-09-07T07:02:13.000Z",
        "timestamp": 1788764533
      }
    },
    {
      "review_id": "6a9abe16910951bc588a6399",
      "review_link": "https://www.trustpilot.com/reviews/6a9abe16910951bc588a6399",
      "rating": 3,
      "title": "We had our broadband updated yesterday",
      "review_text": "We had our broadband updated yesterday, and I am pleased to say that my TV no longer buffers.\nUnfortunately we now have no landline phone.\nCould you please resolve this for us.\nI have just dialled 03337770777 (on my mobile) only to be told the current waiting time is over 30 minutes. \n3225076\n\nPlease don't ask me to reach to your technical  team. The reason I wrote this is because you don't answere the phone! Can you please make them aware of the fault!",
      "review_language": "en",
      "review_datetime_utc": "2026-09-04T14:48:22.000Z",
      "review_timestamp": 1788533302,
      "experience_date": "2026-09-04",
      "updated_datetime_utc": "2026-09-04T15:28:19.000Z",
      "is_verified": false,
      "verification_level": "not-verified",
      "like_count": 0,
      "company_name": "Utility Warehouse",
      "company_domain": "uw.co.uk",
      "company_url": "https://www.trustpilot.com/review/uw.co.uk",
      "business_unit_id": "48e8f676000064000503c337",
      "owner_response": {
        "text": "Hi Phillip,\n\nWe are so pleased to hear that your TV is no longer buffering following your broadband upgrade. However, we are very sorry to hear that your landline is currently not working and that you experienced a long wait time when trying to call us.\n\nWhile we cannot fix this issue directly via this platform, our Technical team will be more than happy to help you get your landline up and running. Please reach out to them so they can look into this for you right away.\n\nThanks,\nThe Utility Warehouse Team",
        "datetime_utc": "2026-09-04T15:02:44.000Z",
        "timestamp": 1788534164
      }
    }
  ],
  "count": 20,
  "page": 1,
  "total_pages": 7
}
```

## Notes

- `user_id` is the `author_id` on any review from Company Reviews, or the ID in a `trustpilot.com/users/<id>` URL.
