# Google AI Mode

Send a prompt to Google's AI Mode and get a structured conversational reply with citation links. Each response includes a `session_token` you can pass to the next call to continue the conversation with prior context.

## Endpoint

```
GET /v1/web/ai-mode
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `prompt` | Yes | The AI Mode prompt (max 2000 characters) |
| `country` | No | 2-letter ISO 3166-1 alpha-2 country code (default: `us`) |
| `language` | No | 2-letter ISO 639-1 language code (default: `en`) |
| `session_token` | No | Token from a previous response to continue the conversation in context |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `reply_parts` | array | Ordered list of structured reply parts. Render them in order to display the answer |
| `reply_parts[].type` | string | Part type: `paragraph`, `heading`, `list`, or `images` |
| `reply_parts[].text` | string | Text content. Present on `paragraph` and `heading` parts |
| `reply_parts[].ordered` | boolean | Present on `list` parts. `true` for numbered lists, `false` for bulleted |
| `reply_parts[].list` | array | Present on `list` parts. Each item is `{title, text}` |
| `reply_parts[].images` | array | Present on `images` parts. Each item is `{url, label, width, height}` |
| `reference_links` | array | Citation sources used in the reply |
| `reference_links[].title` | string | Citation title |
| `reference_links[].link` | string | Citation URL |
| `reference_links[].snippet` | string | Short preview of the cited source |
| `reference_links[].source` | string | Source name |
| `reference_links[].favicon` | string | Source favicon URL |
| `reference_links[].date` | string | Publication date (when available) |
| `session_token` | string | Token to pass in a subsequent request to continue this conversation |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/web/ai-mode?prompt=How%20do%20I%20make%20pizza%3F" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

# First call - new conversation
response = requests.get(
    "https://apidirect.io/v1/web/ai-mode",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"prompt": "How do I make pizza?"}
)
data = response.json()

# Walk the reply_parts to display the answer
for part in data["reply_parts"]:
    if part["type"] in ("paragraph", "heading"):
        print(part["text"])
    elif part["type"] == "list":
        for item in part["list"]:
            print(f"- {item['title']} {item['text']}")

# Follow-up that continues the same conversation
followup = requests.get(
    "https://apidirect.io/v1/web/ai-mode",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "prompt": "What about a gluten-free version?",
        "session_token": data["session_token"]
    }
)
```

## Example Response

```json
{
  "reply_parts": [
    {
      "type": "paragraph",
      "text": "Making pizza at home involves preparing the dough, sauce, and toppings, then baking at high heat."
    },
    {
      "type": "heading",
      "text": "1. Prepare the Dough"
    },
    {
      "type": "list",
      "ordered": false,
      "list": [
        {
          "title": "Activate Yeast:",
          "text": "Mix warm water with yeast and a pinch of sugar. Let it sit for about 5-10 minutes until foamy."
        },
        {
          "title": "Mix and Knead:",
          "text": "Combine the yeast mixture with flour and salt. Knead for 5-10 minutes until smooth and elastic."
        }
      ]
    }
  ],
  "reference_links": [
    {
      "title": "Best Homemade Pizza Dough (photo tutorial)",
      "link": "https://www.crunchycreamysweet.com/the-best-homemade-pizza-dough-photo-tutorial/",
      "snippet": "Instructions. Place water and sugar in a large mixing bowl...",
      "source": "Crunchy Creamy Sweet",
      "favicon": "https://encrypted-tbn1.gstatic.com/faviconV2?url=https://www.crunchycreamysweet.com&size=128",
      "date": "Jul 6, 2012"
    }
  ],
  "session_token": "Q21vd1lUZHFaMjlNYWtOTWREQndWRmRyV1RNemFqRnViak01Ym1FeE1tdFZVemhFVGxCeFQxZE9RV1o0..."
}
```

## Notes

- `reply_parts` is an ordered array of typed blocks. Walk it in order and render each block based on its `type` field. This matches the structure used by the AI Overview inside `/v1/web/search`.
- Image blocks may include base64 placeholder URLs (`data:image/...`) alongside real CDN URLs — filter as needed.
- `session_token` is opaque — treat it as a string and pass it back unchanged to continue the conversation.
- Each follow-up call is billed as a fresh $0.005 request.
