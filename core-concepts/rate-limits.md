# Rate Limits

API Direct enforces concurrency limits to ensure fair usage and reliable performance for all users.

## Concurrency Limit

Each user is limited to **3 concurrent requests per endpoint**. This means you can have up to 3 in-flight requests to the same endpoint at the same time. Requests to different endpoints are counted separately.

For example, you can simultaneously make:
- 3 requests to `/v1/reddit/posts`
- 3 requests to `/v1/twitter/posts`
- 3 requests to `/v1/linkedin/posts`

## 429 Response

If you exceed the concurrency limit, you'll receive a `429` status code:

```json
{
  "error": "Too many concurrent requests for this endpoint",
  "code": "concurrency_limit_exceeded",
  "limit": 3,
  "current": 3
}
```

## Best Practices

**Use sequential requests** - For most use cases, sending requests one at a time is sufficient given the 1-2 second response times.

**Queue your requests** - If you need to make many requests, implement a queue that limits concurrency to 3 per endpoint.

**Use the `pages` parameter** - Endpoints like Twitter, YouTube, and Instagram support fetching multiple pages in a single request, reducing the total number of API calls needed.

**Spread across endpoints** - Concurrency limits are per-endpoint, so requests to different endpoints don't count against each other.

## Need Higher Limits?

If you need higher concurrency limits for your use case, contact us at [support@apidirect.io](mailto:support@apidirect.io).
