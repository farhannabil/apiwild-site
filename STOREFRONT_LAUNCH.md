# Existing-account storefront checkout — 2026-09-26

- Scope: TelePrestige, Legacy TV, Omega TV and Wolves TV prepaid digital packages.
- Account: acct_1UCiHN194XZKj6cF / 2740797 Ontario Inc. No Connect routing or separate onboarding.
- 112 exact CAD selections; 16 brand/product groupings. Prices exclude applicable tax. Canada registration/settings were checked active; CAD15 Ontario sample returned CAD1.95 HST / standard_rated. Existing preset tax code and registrations unchanged.
- Runtime uses the existing protected Stripe credential/webhook. No secrets are exported.
- Checkout requires STOREFRONT_CHECKOUT_ENABLED and WEBHOOK_INGRESS_VERIFIED. Other AI billing/provider gates remain unchanged.
- Browser-supplied prices are ignored. Catalog validation, fixed origins, account checks, durable retry IDs, daily request limits, signed webhooks, paid-only fulfillment and unique per-order queue entries are implemented.
- Activation remains MANUAL through the merchant's Stripe payment record, customer email and exact SKU/term/connection metadata. No automatic TV account provisioning or activation email is claimed. Hardware retains the previous store checkout pending shipping setup.
- Paid orders queue as manual_pending; refunds/disputes flag review_required. Fulfill only Stripe-confirmed paid orders. Do not activate pending/failed/disputed/refunded orders. Existing account-wide receipt/support/legal settings remain unchanged; storefront checkout display names are scoped per session.
- Existing API WILD/AUTO DEVENZO customers, credit orders, payouts and subscriptions are preserved. Clean source checkout avoids publishing unrelated dirty work in apiwild-site.
- Tests and deployment receipts are recorded in Linear GEN-30 / GEN-10. A live completed card payment/refund is not asserted; no customer card is charged during setup.
- AI sales remain gated: AARO has no production AI/billing service; API WILD public gateway reports disabled/all capabilities unavailable. Fahim AI Studio has no approved billing catalog.
