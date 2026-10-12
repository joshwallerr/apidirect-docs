# Substack Publication Recommendations

Get the publications a Substack publication recommends to its readers, and the publications that recommend it. Each entry carries the publication's name, URL, tagline, author, language, paid status and the recommender's blurb.

## Endpoint

```
GET /v1/substack/publication/recommendations
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
| `publication` | object | The publication (`publication_id`, `name`, `subdomain`, `url`, `logo_url`) |
| `recommends` | array | Publications this publication recommends |
| `recommends[].publication_id` | string | Publication ID |
| `recommends[].name` | string | Publication name |
| `recommends[].subdomain` | string | Substack subdomain |
| `recommends[].url` | string | Publication home URL |
| `recommends[].logo_url` | string | Logo URL |
| `recommends[].description` | string | Publication tagline |
| `recommends[].author` | string | Primary author's handle |
| `recommends[].author_name` | string | Primary author's display name |
| `recommends[].author_id` | string | Primary author's user ID |
| `recommends[].author_url` | string | Link to the primary author's profile |
| `recommends[].language` | string | Language code |
| `recommends[].paid_enabled` | boolean | Whether paid subscriptions are enabled |
| `recommends[].blurb` | string | The recommender's note about the publication, empty when none |
| `recommends[].date` | string | Date the recommendation was made (UTC) |
| `recommended_by` | array | Publications that recommend this publication (the most recent 50), same fields |
| `recommends_count` | integer | Number of outgoing recommendations returned |
| `recommended_by_count` | integer | Number of incoming recommendations returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/publication/recommendations?publication=lenny" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/publication/recommendations",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"publication": "lenny"}
)
print(response.json())
```

## Example Response

```json
{
  "publication": {
    "logo_url": "https://substackcdn.com/image/fetch/$s_!8MSN!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F…",
    "name": "Lenny's Newsletter",
    "publication_id": "10845",
    "subdomain": "lenny",
    "url": "https://www.lennysnewsletter.com"
  },
  "recommended_by": [
    {
      "author": "deepthiconnects",
      "author_id": "496409115",
      "author_name": "Deepthi",
      "author_url": "https://substack.com/@deepthiconnects",
      "blurb": "",
      "date": "2026-10-11 04:59:17",
      "description": "My personal Substack",
      "language": "en-gb",
      "logo_url": "https://substack-post-media.s3.amazonaws.com/public/images/3e9d7ce7-391a-454e-b54e-a5732b0dde33_1254x1254.png",
      "name": "YStartUps",
      "paid_enabled": false,
      "publication_id": "11624830",
      "subdomain": "ystartups",
      "url": "https://ystartups.substack.com"
    }
  ],
  "recommended_by_count": 50,
  "recommends": [
    {
      "author": "merlindotinc",
      "author_id": "510813323",
      "author_name": "Merlin",
      "author_url": "https://substack.com/@merlindotinc",
      "blurb": "",
      "date": "2026-05-25 20:11:01",
      "description": "learn about silicon valley companies, people, jobs, and ideas through the eyes of two startup junkies.",
      "language": "",
      "logo_url": "https://substack-post-media.s3.amazonaws.com/public/images/1e2e78d1-1693-48ab-9755-ea88a06e2f23_1080x1080.png",
      "name": "early days",
      "paid_enabled": false,
      "publication_id": "9047553",
      "subdomain": "earlydaysbymerlin",
      "url": "https://earlydaysbymerlin.substack.com"
    }
  ],
  "recommends_count": 11
}
```
