# Pricing

API Direct uses a pay-per-request pricing model. There are no monthly fees, subscriptions, or minimum commitments.

## Free Tier

Every account gets **50 free requests per endpoint per month**. No credit card required. Free requests reset on the 1st of each month.

## Price Table

| Endpoint | Price | Unit |
|----------|-------|------|
| LinkedIn Posts | $0.006 | per request |
| Twitter Posts | $0.006 | per page |
| Reddit Posts | $0.003 | per request |
| Reddit Comments | $0.003 | per page |
| YouTube Videos | $0.005 | per page |
| Instagram Posts | $0.006 | per page |
| TikTok Videos | $0.006 | per page |
| Forum Posts | $0.008 | per request |
| News Articles | $0.008 | per request |

## How Billing Works

- You are only charged for **successful requests** (2xx responses)
- Failed requests (4xx, 5xx) are not billed
- For multi-page endpoints (Twitter, Reddit Comments, YouTube, Instagram, TikTok), you are billed per page fetched
- Charges accumulate and are billed when your balance reaches a threshold

## Trust Levels

Your account has a trust level that determines your billing threshold:

| Trust Level | Billing Threshold | How to Reach |
|-------------|------------------|--------------|
| New | $10 | Default for new accounts |
| Tier 1 | $100 | After successful payment history |
| Tier 2 | $250 | After continued payment history |
| Trusted | End of month | After consistent payment history |

When your accumulated charges reach your billing threshold, your card is charged automatically. Trusted accounts are billed at the end of each month instead of at a fixed threshold.

## Adding a Payment Method

To use the API beyond the free tier, add a credit or debit card in your [billing dashboard](https://apidirect.io/dashboard/billing). You can also set [spending limits](spending-limits.md) to control your costs.
