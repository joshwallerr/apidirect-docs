# Response Format

All endpoints return a consistent JSON structure, making it easy to work with data from multiple platforms using the same code.

## Standard Response Shape

```json
{
  "posts": [
    {
      "title": "Post title or heading",
      "url": "https://platform.com/post/...",
      "date": "2024-06-15 14:30:00",
      "author": "username",
      "source": "Platform Name",
      "domain": "platform.com",
      "snippet": "Content preview or excerpt..."
    }
  ],
  "page": 1,
  "count": 20
}
```

## Core Fields

Most post objects contain these fields:

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Post title or formatted heading |
| `url` | string | Direct link to the original post |
| `date` | string | Publication date (`YYYY-MM-DD HH:MM:SS`). Not returned by Forum Posts or News Articles. |
| `author` | string | Author name or username. Not returned by Forum Posts or News Articles (News uses `authors` array). |
| `source` | string | Platform name (e.g., "Reddit", "LinkedIn") |
| `domain` | string | Platform domain (e.g., "reddit.com", "linkedin.com") |
| `snippet` | string | Content text or preview |

## Pagination Fields

Depending on the endpoint, responses include either `page` (current page number) or `pages` (number of pages fetched), plus a `count` of total results returned.

| Field | Type | Description |
|-------|------|-------------|
| `page` | integer | Current page number (used by LinkedIn, Reddit Posts, Forum Posts) |
| `pages` | integer | Number of pages fetched (used by Twitter, Reddit Comments, YouTube, Instagram) |
| `limit` | integer | Requested result limit (used by News Articles) |
| `count` | integer | Total number of results returned |

## Platform-Specific Fields

Some endpoints include additional fields:

| Field | Endpoints | Description |
|-------|-----------|-------------|
| `subreddit` | Reddit Posts, Reddit Comments | The subreddit name |
| `type` | Reddit Comments | Content type (`"comment"`) |
| `position` | Forum Posts | Result ranking position |
| `rank` | Forum Posts | Result rank value |
| `authors` | News Articles | List of author names |
| `photo_url` | News Articles | Article photo URL |
| `thumbnail_url` | News Articles | Article thumbnail URL |
| `published_datetime_utc` | News Articles | Publication date and time in UTC |
| `source_name` | News Articles | News source name |
| `source_url` | News Articles | News source URL |
| `source_favicon_url` | News Articles | News source favicon URL |

## Full Example

```json
{
  "posts": [
    {
      "title": "Best practices for API design",
      "url": "https://reddit.com/r/programming/comments/abc123",
      "date": "2024-06-15 14:30:00",
      "author": "dev_user",
      "source": "Reddit",
      "domain": "reddit.com",
      "subreddit": "programming",
      "snippet": "After building dozens of APIs, here are the patterns that work best..."
    },
    {
      "title": "Why REST still matters in 2024",
      "url": "https://reddit.com/r/webdev/comments/def456",
      "date": "2024-06-14 09:15:00",
      "author": "web_architect",
      "source": "Reddit",
      "domain": "reddit.com",
      "subreddit": "webdev",
      "snippet": "Despite the rise of GraphQL, REST APIs continue to be the standard..."
    }
  ],
  "page": 1,
  "count": 20
}
```
