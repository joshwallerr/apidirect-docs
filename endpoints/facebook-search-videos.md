# Facebook Search Videos

Search for Facebook videos by keyword. Returns video details including title, description, author information, thumbnail, and view metrics.

## Endpoint

```
GET /v1/facebook/videos
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |
| `start_date` | No | Filter videos from this date onward (format: `YYYY-MM-DD`) |
| `end_date` | No | Filter videos up to this date (format: `YYYY-MM-DD`) |
| `sort_by` | No | Sort order: `most_recent` or `relevance` (default: `relevance`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `videos` | array | Array of matching Facebook videos |
| `videos[].video_id` | string | Unique video identifier |
| `videos[].video_url` | string | Direct link to the video |
| `videos[].title` | string/null | Video title |
| `videos[].description` | string | Video description text |
| `videos[].author_name` | string | Name of the video uploader |
| `videos[].author_url` | string | Link to the author's profile or page |
| `videos[].author_verified` | boolean | Whether the author is verified |
| `videos[].thumbnail` | string | URL of the video thumbnail image |
| `videos[].time_and_views` | string/null | Display string showing upload time and view count |
| `count` | integer | Number of videos returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/videos?query=cooking" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/videos",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "cooking"
    }
)
print(response.json())
```

## Example Response

```json
{
  "videos": [
    {
      "video_id": "1048293756182940",
      "video_url": "https://www.facebook.com/watch/?v=1048293756182940",
      "title": "Easy 15-Minute Pasta Recipe",
      "description": "Learn how to make this delicious creamy garlic pasta in just 15 minutes! Perfect for busy weeknight dinners.",
      "author_name": "Tasty",
      "author_url": "https://www.facebook.com/buzzfeedtasty",
      "author_verified": true,
      "thumbnail": "https://scontent.fxxx.fbcdn.net/v/t15.5256-10/pasta_thumbnail.jpg",
      "time_and_views": "2 days ago · 1.2M views"
    },
    {
      "video_id": "8374920183746251",
      "video_url": "https://www.facebook.com/watch/?v=8374920183746251",
      "title": "Gordon Ramsay's Top 5 Cooking Tips",
      "description": "Master chef Gordon Ramsay shares his essential cooking tips that every home cook should know.",
      "author_name": "Gordon Ramsay",
      "author_url": "https://www.facebook.com/gordonramsay",
      "author_verified": true,
      "thumbnail": "https://scontent.fxxx.fbcdn.net/v/t15.5256-10/ramsay_tips_thumbnail.jpg",
      "time_and_views": "1 week ago · 4.5M views"
    },
    {
      "video_id": "5928371640192837",
      "video_url": "https://www.facebook.com/watch/?v=5928371640192837",
      "title": "Homemade Sourdough Bread from Scratch",
      "description": "Step-by-step guide to baking the perfect sourdough loaf at home. No experience needed!",
      "author_name": "Home Baking Club",
      "author_url": "https://www.facebook.com/HomeBakingClub",
      "author_verified": false,
      "thumbnail": "https://scontent.fxxx.fbcdn.net/v/t15.5256-10/sourdough_thumbnail.jpg",
      "time_and_views": "3 weeks ago · 287K views"
    }
  ],
  "count": 3,
  "pages": 1
}
```
