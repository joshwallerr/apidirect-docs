# Error Handling

When a request fails, API Direct returns a JSON error response with an HTTP status code, an `error` message, and a `code` identifier.

## Error Response Format

```json
{
  "error": "Human-readable error message",
  "code": "machine_readable_code"
}
```

## Error Codes

| Status | Code | Description |
|--------|------|-------------|
| `401` | `missing_api_key` | No `X-API-Key` header was provided |
| `401` | `invalid_api_key` | The API key is invalid, revoked, or deleted |
| `401` | `user_not_found` | The user account associated with the key was not found |
| `402` | `payment_required` | Free tier exhausted and no payment method on file |
| `403` | `account_blocked` | Account blocked due to payment failure |
| `429` | `daily_limit_exceeded` | Daily spending limit reached |
| `429` | `monthly_limit_exceeded` | Monthly spending limit reached |
| `429` | `concurrency_limit_exceeded` | Too many concurrent requests to this endpoint |
| `502` | `upstream_error` | The data source returned an error |
| `504` | `upstream_timeout` | The data source did not respond in time |

## Handling Errors

### Authentication Errors (401)

Check that you're including the `X-API-Key` header and that your key is valid and active. You can verify your keys in the [dashboard](https://apidirect.io/dashboard/keys).

### Payment Errors (402, 403)

A `402` means your free tier is exhausted and you need to add a payment method. A `403` with `account_blocked` means a previous payment failed — update your card in the [billing dashboard](https://apidirect.io/dashboard/billing).

### Rate Limits and Spending Limits (429)

A `429` with `concurrency_limit_exceeded` means you have too many in-flight requests to the same endpoint. Wait for current requests to complete. See [Rate Limits](/docs/rate-limits) for details.

A `429` with `daily_limit_exceeded` or `monthly_limit_exceeded` means you've hit a spending cap. See [Spending Limits](/docs/spending-limits).

### Upstream Errors (502, 504)

These indicate a temporary issue with the data source. Retry after a short delay (1-2 seconds). If the error persists, the platform may be experiencing an outage.

## Retry Strategy

For transient errors (`502`, `504`, `429`), we recommend:

1. Wait 1-2 seconds before retrying
2. Use exponential backoff for repeated failures
3. Set a maximum of 3 retries per request
