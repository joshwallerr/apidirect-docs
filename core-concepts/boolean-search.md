# Boolean Search

Your `query` is passed straight through to each platform's own search engine, so on supported endpoints you can use that platform's boolean operators — exact phrases (`"..."`), `OR`, exclusion (`-term`), and grouping `( )` — to build precise queries.

Operators like `OR`, `AND`, and `NOT` must be **UPPERCASE**; lowercase is treated as an ordinary search word.

## Endpoints that support boolean operators

| Endpoint | Operator reference |
|----------|--------------------|
| `/v1/reddit/posts` | [Reddit search operators](https://support.reddithelp.com/hc/en-us/articles/19696541895316-Available-search-features) — `AND` `OR` `NOT` `-` `( )`, fields like `subreddit:` `author:` |
| `/v1/twitter/posts` | [X advanced search](https://help.x.com/en/using-x/x-advanced-search) — phrases, `OR`, `-`, `( )`, fields like `from:` `filter:` (use `-`, not `NOT`) |
| `/v1/forums/posts` | [Google search operators](https://support.google.com/websearch/answer/2466433) — phrases, `OR`/`\|`, `-`, `( )`, `site:` (use `-`, not `NOT`) |
| `/v1/linkedin/posts` | [LinkedIn boolean search](https://www.linkedin.com/help/linkedin/answer/a524335) — `AND` `OR` `NOT` `-` `( )` (phrases are matched loosely) |

```bash
curl -G "https://apidirect.io/v1/reddit/posts" \
  --data-urlencode 'query=(remote OR hybrid) engineer -recruiter' \
  -H "X-API-Key: YOUR_API_KEY"
```

## Everything else is keyword search

`/v1/youtube/posts`, `/v1/facebook/posts`, `/v1/instagram/posts`, and `/v1/tiktok/videos` don't support operators — they run relevance-based keyword search, so any operator you include is treated as literal text. Pass plain keywords instead. (On YouTube and Facebook every word must appear; Instagram and TikTok match loosely.)
