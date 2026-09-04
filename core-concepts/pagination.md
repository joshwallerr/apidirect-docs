# Pagination

API Direct endpoints support pagination to retrieve multiple pages of results. There are two pagination patterns depending on the endpoint.

## Pattern 1: `page` Parameter

Some endpoints use a `page` parameter where you request one page at a time. Each request returns a single page of results.

**Endpoints using `page`:** LinkedIn Posts, Reddit Posts, Forum Posts

```bash
# Get page 1
curl "https://apidirect.io/v1/reddit/posts?query=python&page=1" \
  -H "X-API-Key: YOUR_API_KEY"

# Get page 2
curl "https://apidirect.io/v1/reddit/posts?query=python&page=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

The response includes the current `page` number:

```json
{
  "posts": [...],
  "page": 2,
  "count": 20
}
```

## Pattern 2: `pages` Parameter

Other endpoints use a `pages` parameter that fetches multiple pages in a single API call. This is useful for retrieving larger result sets without making multiple requests.

**Endpoints using `pages`:** Twitter Posts, Facebook (all paginated endpoints), Reddit Comments, YouTube Videos, Instagram (posts, user posts, followers, following, post comments, comment replies, hashtag posts), TikTok Videos, Web Search

```bash
# Fetch 3 pages of results in one call
curl "https://apidirect.io/v1/twitter/posts?query=AI&pages=3" \
  -H "X-API-Key: YOUR_API_KEY"
```

The response includes the number of `pages` fetched:

```json
{
  "posts": [...],
  "pages": 3,
  "count": 60
}
```

## Page Limits

| Endpoint | Param | Max Pages |
|----------|-------|-----------|
| LinkedIn Posts | `page` | 25 |
| LinkedIn Person Posts | `page` | 30 |
| LinkedIn Company Posts | `page` | 50 |
| LinkedIn Companies | `page` | 100 |
| LinkedIn Jobs | `page` | 40 |
| Reddit Posts | `page` | 12 |
| Forum Posts | `page` | 10 |
| Twitter (all paginated endpoints except following) | `pages` | 20 |
| Twitter User Following | `pages` | 175 |
| Facebook (page posts/photos/videos/reviews, group posts, search posts/pages/videos/events) | `pages` | 15 |
| Facebook Post Comments | `pages` | 20 |
| Facebook Page Reels, Group Search | `pages` | 10 |
| Reddit Comments | `pages` | 10 |
| YouTube Videos | `pages` | 20 |
| YouTube Channels | `pages` | 20 |
| YouTube Comments | `pages` | 20 |
| Truth Social User Posts | `pages` | 20 |
| Instagram Posts | `pages` | 20 |
| Instagram User Posts | `pages` | 20 |
| Instagram User Followers | `pages` | 40 |
| Instagram User Following | `pages` | 40 |
| Instagram Post Comments | `pages` | 20 |
| Instagram Comment Replies | `pages` | 10 |
| Instagram Hashtag Posts | `pages` | 10 |
| TikTok Videos | `pages` | 10 |
| Web Search | `pages` | 10 |

## Pattern 3: `limit` Parameter

The News Articles endpoint uses a `limit` parameter to control how many results are returned per request (1-100, default 10). Unlike `page` or `pages`, this is not paginated — you get up to `limit` results in a single call.

**Endpoints using `limit`:** News Articles

```bash
# Get 50 news articles
curl "https://apidirect.io/v1/news/articles?query=technology&limit=50" \
  -H "X-API-Key: YOUR_API_KEY"
```

The response includes the requested `limit` and actual `count`:

```json
{
  "articles": [...],
  "limit": 50,
  "count": 50
}
```

## Billing Note

For endpoints using the `pages` parameter, you are billed per page fetched. For example, requesting `pages=3` on the Twitter endpoint costs 3x the per-page price.

The News Articles endpoint is billed as a single request regardless of the `limit` value.

## Endpoints Without Pagination

Some endpoints return everything the platform exposes in a single billed request, so they take no pagination parameter at all: Instagram User Stories, Instagram User Highlights, Instagram Highlight Stories, and Instagram Post Likes.
