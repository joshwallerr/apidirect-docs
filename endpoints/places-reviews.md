# Place Reviews

Get user reviews for a place by `place_id`. Each review includes the rating, full review text, author info (with photo URL and total review count), timestamps, attached photos, and any owner response.

## Endpoint

```
GET /v1/places/reviews
```

**Price:** $0.01 per page
**Free tier:** 20 requests/month

Each page returns up to 10 reviews.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `place_id` | Yes | Google `place_id`, as returned by the [Places Search](/docs/places-search) endpoint |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1). Each page returns up to 10 reviews and is billed as one request |
| `sort_by` | No | `most_relevant` (default), `newest`, `highest_ranking`, `lowest_ranking` |
| `language` | No | 2-letter ISO 639-1 language code (default: `en`). Returns only reviews originally written in this language |
| `translate_reviews` | No | Set to `true` to translate the returned reviews into the requested `language` |
| `country` | No | 2-letter ISO 3166-1 alpha-2 region code (default: `us`) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis to each review (+$0.001/request) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `reviews` | array | Array of reviews |
| `reviews[].review_id` | string | Stable review identifier |
| `reviews[].rating` | integer | Star rating, 1-5 |
| `reviews[].review_text` | string | Review body text |
| `reviews[].review_datetime_utc` | string | ISO 8601 review datetime (UTC) |
| `reviews[].review_timestamp` | integer | Unix timestamp (seconds) |
| `reviews[].review_time` | string | Human-readable relative time (e.g. `3 months ago`) |
| `reviews[].review_link` | string | Direct link to the review on Google Maps |
| `reviews[].review_photos` | array | Array of photo URLs attached to the review |
| `reviews[].review_language` | string | Detected review language code |
| `reviews[].review_text_translated_language` | string \| null | Target language code if the review has been translated |
| `reviews[].like_count` | integer | Number of "likes" the review has received |
| `reviews[].review_source` | string | Source platform name (typically `Google`) |
| `reviews[].review_source_logo` | string | Source platform logo URL |
| `reviews[].author_id` | string | Google contributor ID |
| `reviews[].author_name` | string | Review author display name |
| `reviews[].author_link` | string | Author Google Maps profile URL |
| `reviews[].author_photo_url` | string \| null | Author profile photo URL |
| `reviews[].author_review_count` | integer | Total reviews this author has posted |
| `reviews[].author_photo_count` | integer | Total photos this author has uploaded |
| `reviews[].author_reviews_link` | string | URL to all of this author's reviews |
| `reviews[].author_is_local_guide` | boolean | Whether the author is a Google Local Guide |
| `reviews[].author_local_guide_level` | integer \| null | Local Guide level (1-10) if applicable |
| `reviews[].owner_response` | object \| null | Object with `text`, `datetime_utc`, `timestamp`, `time`, `language` when the place owner has responded |
| `reviews[].sentiment` | object | Emotion analysis: `emotions`, `dominant_emotion`, `emotional_intensity`, `polarity` (when `get_sentiment=true`) |
| `count` | integer | Number of reviews returned |
| `pages` | integer | Echo of requested pages |
| `sort_by` | string | Echoed sort order |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/places/reviews?place_id=ChIJifIePKtZwokRVZ-UdRGkZzs&pages=2&sort_by=newest" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/places/reviews",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "place_id": "ChIJifIePKtZwokRVZ-UdRGkZzs",
        "pages": 2,
        "sort_by": "newest"
    }
)
print(response.json())
```

## Example Response

```json
{
  "reviews": [
    {
      "review_id": "Ci9DQUlRQUNvZENodHljRjlvT2pWeU1rdFZhREZPY214dmRVSlplRzQ0ZURWVk9XYxAB",
      "rating": 5,
      "review_text": "Amazing pizza, fast service. Highly recommend.",
      "review_datetime_utc": "2026-02-15T12:05:54.947Z",
      "review_timestamp": 1771157154,
      "review_time": "3 months ago",
      "review_link": "https://www.google.com/maps/reviews/...",
      "review_photos": ["https://lh3.googleusercontent.com/grass-cs/..."],
      "review_language": "en",
      "review_text_translated_language": "en",
      "like_count": 0,
      "review_source": "Google",
      "review_source_logo": "https://www.gstatic.com/images/branding/product/1x/googleg_48dp.png",
      "author_id": "103696814314978516852",
      "author_name": "Salman Idrees",
      "author_link": "https://www.google.com/maps/contrib/103696814314978516852",
      "author_photo_url": "https://lh3.googleusercontent.com/a-/ALV-...",
      "author_review_count": 392,
      "author_photo_count": 356,
      "author_reviews_link": "https://www.google.com/maps/contrib/103696814314978516852/reviews",
      "author_is_local_guide": true,
      "author_local_guide_level": 7,
      "owner_response": null
    }
  ],
  "count": 1,
  "pages": 2,
  "sort_by": "newest"
}
```

## Getting more reviews

Beyond increasing the `pages` parameter, two knobs surface different review sets:

**1. `sort_by`** — four options, each returns a different set of reviews:

- `most_relevant` (default) — Google's relevance ranking
- `newest` — reverse chronological order
- `highest_ranking` — 5-star and 4-star reviews first
- `lowest_ranking` — 1-star and 2-star reviews first

**2. `language`** — filters reviews to those originally written in that language. The same `place_id` returns a different set of reviews for each language.

Combining all four sort orders with a handful of languages can surface several hundred reviews per place.

To consolidate the multilingual set in one language, add `translate_reviews=true` and the returned reviews will be translated into your chosen `language`.

## Notes

- If a place has no reviews in the requested `language`, the response is empty (still billed as one request).
- `translate_reviews=true` replaces each review's text with the translation. The `review_language` field shows the original language; `review_text_translated_language` matches your target.
- The `owner_response` field is `null` when the business owner has not replied to the review.
- Set `get_sentiment=true` to add per-review emotion analysis to the response.
