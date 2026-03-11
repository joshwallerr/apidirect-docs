# Pricing

API Direct uses a pay-per-request pricing model. There are no monthly fees, subscriptions, or minimum commitments.

## Free Tier

Every account gets **50 free requests per endpoint per month**. No credit card required. Free requests reset on the 1st of each month.

## Pricing by Platform

Prices range from **$0.003 to $0.008 per request** depending on the endpoint. Each endpoint's documentation page shows its exact price.

| Platform | Price per Request |
|----------|------------------|
| Reddit | $0.003 |
| YouTube | $0.005 |
| LinkedIn, Twitter/X, Instagram, TikTok | $0.006 |
| Facebook, Forums, News | $0.008 |

## How Billing Works

- You are only charged for **successful requests** (2xx responses)
- Failed requests (4xx, 5xx) are not billed
- For multi-page endpoints (Twitter Search/Tweets/Followers/etc., Reddit Comments, YouTube, Instagram, TikTok), you are billed per page fetched
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

To use the API beyond the free tier, add a credit or debit card in your [billing dashboard](https://apidirect.io/dashboard/billing). You can also set [spending limits](/docs/spending-limits) to control your costs.
