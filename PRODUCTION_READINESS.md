# API WILD production readiness — 2026-09-26

## Production services

| Area | Current production state | Evidence | Activation decision |
|---|---|---|---|
| Public Site | Deployed and reachable | `https://apiwild.com/` returns HTTP 200; Sites project `appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d` | Active |
| Customer Auth | Public signup enabled; email/password enabled; email confirmation required; anonymous users disabled | Supabase Auth public settings on project `yautmilnpllojugpmfgy` | Active, owner mailbox acceptance still required |
| Postgres profile data | `customer_profiles` RLS enabled | SELECT/INSERT/UPDATE policies require `auth.uid() = user_id`; UPDATE has both `USING` and `WITH CHECK` | Active |
| Customer lifecycle | Signup, callback, login, onboarding, local signout, recovery, session restore implemented | Automated auth, profile, isolation, and recovery tests pass | Active, real second-browser owner test outstanding |
| Auth email | Confirmation/recovery/invite/magic-link templates prepared; autoconfirm is false | Email provider enabled in public Auth settings; template tests pass | Active, real delivery acceptance outstanding |
| Support email | Resend inbound webhook and acknowledgement | `support-inbound` Edge Function ACTIVE version 5; prior owner inbox/replay evidence; SPF/DKIM/DMARC DNS present | Active |
| Stripe account | Live account `2740797 ONTARIO INC.` available | Dashboard setup shows identity, live API keys, payments, product catalog, payment link, Tax registration, and integration choices completed | Connected, customer checkout held |
| Stripe backend | Checkout, customer, portal, invoices, receipts, webhook, exactly-once ledger, refund, dispute and failed-payment reconciliation implemented | Stripe 2026-08-26.dahlia; signature and lifecycle tests pass | Connected, fail-closed |
| Stripe email | Stripe-native receipt/invoice and refund messages are canonical | Custom duplicate financial templates remain intentionally suppressed | Activates with accepted checkout lifecycle |
| Sites D1 | Production schema present | Billing customers/orders/events/disputes, credit ledger, gateway requests/outbox/keys/accounts/audio, profiles/preferences/briefs | Active |
| SubRouter inference | Adapter deployed but no paid station or credential | `/api/gateway/config` reports all capabilities unavailable | Deferred by owner |

## Verified production security controls

- Secrets are stored only as Sites secret environment variables and are not returned to the browser.
- Supabase browser configuration exposes only the project URL and publishable key.
- Billing requires a confirmed, non-anonymous Supabase user and a completed customer profile.
- Stripe webhook signatures are verified before processing.
- Fulfilment uses verified Stripe session state, not the success page.
- Checkout and webhook processing are idempotent and exactly-once at the credit ledger.
- Refunds reverse only verified credits; disputes hold available credit.
- Checkout uses dynamic payment methods and the latest configured Stripe API version.
- Customer billing and inference remain independent: customers cannot buy unusable inference credit while SubRouter is deferred.

## Current intentional production gates

- `COMMERCE_READY=false` until one owner-controlled live or authorized test lifecycle proves checkout, webhook credit, receipt/invoice, refund, dispute handling, and no-return recovery.
- `BILLING_ENABLED=false` while inference remains unavailable, preventing sale of unusable credits.
- `GATEWAY_ENABLED=false` and `GATEWAY_ACCEPTANCE_VERIFIED=false` until the SubRouter purchase, credential, bounded calls, receipts, and debits are accepted.
- Supabase leaked-password protection remains disabled and should be enabled in Authentication → Attack Protection before the public launch announcement.
- Do not claim owner email delivery, second-browser persistence, or recovery acceptance until Farhan completes the real mailbox/browser flow.

## Owner acceptance runbook

1. Create an API WILD account with an owner-controlled email address.
2. Open the real confirmation email and verify the callback returns to `apiwild.com`.
3. Complete onboarding and save the profile.
4. Sign out locally, open a fresh browser session, sign in, and verify the saved profile.
5. Request password recovery, set a new password personally, and sign in again.
6. After SubRouter inference is accepted, authorize one $5 USD Stripe purchase.
7. Verify exactly one credit, Stripe receipt/invoice delivery, one bounded provider response/debit, a refund, and dispute/no-return reconciliation.
8. Only then set `BILLING_ENABLED=true`, `COMMERCE_READY=true`, `GATEWAY_ENABLED=true`, and `GATEWAY_ACCEPTANCE_VERIFIED=true` and redeploy.

