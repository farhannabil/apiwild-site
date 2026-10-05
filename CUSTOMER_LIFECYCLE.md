## Production regression result — 2026-09-08

1. Site/service: https://apiwild.com; Supabase support receiver on verified project `yautmilnpllojugpmfgy`.
2. GitHub: `farhannabil/api-wild`; draft PR https://github.com/farhannabil/api-wild/pull/1 now head `4e0931c4a2daa2421a21f2634ee756bff204a89a`. All 33 changed/exported source files match reviewed Sites source exactly; obsolete migration filename removed. Main remains `06d05055c7d5cb228287c857fecba6867eb4442e`; no merge or successful CI/CD is claimed.
3. Production commit: `841254ad40ceb1eb5545f7ca0b374bce7cd7c4e4`, version **20**, deployed successfully. Version 19 was verified before editing; its signup/password/auth-mail behavior is preserved.
4. Linear: GEN-10, https://linear.app/genxintel/issue/GEN-10/build-ai-model-api-resale-platform. Read/updated before edits; final release results recorded in the issue.
5. Owner: Gen X Intel / Farhan Nabil. Live activation approval is already granted; do not ask for the same approval again.
6. Deployment evidence: saved version `appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d~appgver_05b449f79a2c819186efd43682da78a6`; deployment `appgdep_6aa01eaa8a3c8191ad6d03fd280b752a` succeeded at 2026-09-08T14:42:01.787792+00:00, environment revision 6, public audience retained. Support-inbound version **5** ACTIVE with retrieved exact three-file source parity, JWT setting unchanged and custom signature authentication preserved.

Four parallel audits completed. Fixed finished-checkout retry cleanup, refund result messaging, unrelated Stripe event retries, cross-account cached-profile saves, malformed profile data, support body-size enforcement, and denied planning-save guidance. All **64 source tests** passed; TypeScript zero diagnostics; production build passed. No local preview configuration was packaged. Post-release 11 HTTP health checks and 30 additional page/access-boundary checks passed, as did support oversized-request rejection (413). Five email DNS checks passed independently via public DNS over HTTPS; the local native DNS resolver remains unavailable. These are not real-inbox or paid-customer end-to-end acceptance.

The Supabase daily cron succeeded today at 13:17 UTC. Existing daily maintenance task updated without duplicating its schedule. New GitHub PR run https://github.com/farhannabil/api-wild/actions/runs/34240101119 completed **failure**: build-and-test job `102107759785` failed with zero steps at 14:43:28–14:43:30 UTC; production-health was correctly skipped for the PR event. Four observed runs, zero successful CI runs. The earlier billing-lock evidence remains unresolved; no bypass, forced rerun, migration or fabricated GitHub CD.

**Full paid-service launch is not complete.** Post-release Stripe webhook probe still returned **503 `{"error":"Webhook not configured."}`**. Live Stripe account is already enabled, but secure Site runtime settings remain unavailable to the connected editor and the existing Stripe browser security challenge is incomplete. Actual Checkout, receipt/invoice delivery, terminal failure, partial/full refund and no-return signed webhook acceptance have not run. The source also lacks inference execution and atomic credit spending; six advanced customer-console sections remain inactive. Canonical Stripe financial senders are selected, custom alternatives suppressed; existing branded Auth and deduplicated support remain active. No arbitrary charge/refund, new customer email, disabled business trigger or inference activation occurred.

The detailed architecture, tested cases, limitations and exact owner/action/closing-evidence mapping are in PRODUCTION_REVIEW_2026-09-08.md. The latest user requested no continuation prompt. Historical continuation instructions below are superseded.

## Connection update — 2026-09-07

The user successfully connected Supabase during this repair. This supersedes earlier unavailable/not-connected statements below. However, the active execution registry still exposes zero Supabase tools, and no tool-search capability is available to load them. Do not ask the user to install/reconnect. Resume provider checks when the newly connected tools are exposed in a refreshed turn. No database/provider change is claimed from connection alone.

# Current acceptance status

## Branding and account repair — 2026-09-07

- Recovered latest remote source 9284044 before editing; preserved its Supabase public auth implementation.
- Replaced the orbit logo with a minimal graphite API WILD wordmark and geometric W mark; matching favicon/workspace mark, and a professional dark footer with grouped navigation and legal links.
- Standardized API WILD casing and corrected stale ChatGPT onboarding, account-storage and activation claims on customer-facing information pages. Preserved provider names such as OpenAI where they identify actual catalog providers.
- Implemented forgot-password/reset screens, confirmation landing, resend email, expired-link feedback, connection retries, profile payload validation, save acknowledgement, failed-load protection, console retries/signout errors and mobile navigation.
- Prepared API WILD confirmation/recovery email templates and exact Supabase activation checklist; NOT applied to the provider.
- Validation: production build and TypeScript passed; 15 existing fixture tests plus 3 auth-config/validation regression tests passed; workspace JS syntax and diff whitespace passed. Browser verified logo/footer, email signup/login screens, password-recovery navigation, unavailable config state and expired-confirmation feedback. No real signup, email delivery, live database writes, second-session persistence or mobile browser emulation was verified.
- Blocker: Supabase is not connected this turn. Site runtime read returned project_not_found; local preview has no Supabase config; attempted public config HTTP read returned 403. Do not infer production configuration from local preview. Owner: Gen X Intel / API WILD engineering. Exact prerequisites and closing checks: supabase/AUTH_RELEASE_CHECKLIST.md.
- Linear GEN-10 read/update unavailable; plugin not installed. Local evidence retained; owner to reconnect for synchronization. GitHub farhannabil/api-wild contents API reports repository empty; source linkage missing. No unrelated repository was changed.
- Existing Site edit requested; no publication request in this turn. Save prepared changes without claiming deployment. Customer API-key/usage/billing/brief migration remains incomplete and inactive.

# API WILD — customer lifecycle and activation

## Current public-access state — 2026-09-07

### Supabase connection checkpoint

The active intended project is `api-wild-production` in Canada. `customer_profiles` is RLS-protected and tied to `auth.users`; Site runtime includes the Supabase URL and publishable key only. Public signup/login/onboarding/signout and persistent browser-session code are implemented. Owner-controlled real email confirmation and second-session acceptance remain pending. Stripe and inference are not configured.

`https://apiwild.com` is attached to the Site and reports active provider routing and SSL. The Site audience was changed from an internal two-user custom policy to public access (policy revision 4), so customer entry pages are reachable. This does not itself create customer identity, payments, inference, or entitlement.

Supabase is the intended public identity provider. The connected workspace exposes only an inactive project, `bheheypylmibuicqtywx` (`supabase-aquamarine-elephant`), not verified as API Wild infrastructure. Do not restore or use it until the owner confirms. The hosted runtime has no Supabase URL/publishable key or Stripe credentials, so the existing ChatGPT path remains the only implemented identity path and billing remains disabled.

## Actual journey
/signup → Supabase confirmation email → /login → /onboarding → /console/overview. Supabase restores the browser session and RLS-owned profile on a later visit; signout clears the current browser session. Usage, API keys, billing, provider access and inference remain visibly disabled until their server-side migration and production providers are verified. API WILD does not store customer passwords; Supabase owns credential handling.

## Database
profiles, briefs (existing); preferences, api_keys, usage_events, billing_orders, credit_ledger (0001 additive migration). No model request body is stored. Raw key secrets are not stored. Billing uses integer USD cents, usage uses integer microdollars, and the credit balance is derived from immutable ledger sums. There is no wallet debit/inference execution path yet.

## Runtime configuration prerequisites
Native environment read on 2026-09-06 returned zero entries. No credentials are supplied or inferred.
- STRIPE_SECRET_KEY: account-authorized Stripe test secret in Site runtime secret storage, never source or chat.
- STRIPE_WEBHOOK_SECRET: exact endpoint signing secret in runtime secret storage.
- SITE_ORIGIN: canonical verified Site origin (code defaults to this existing Site).
- WEBHOOK_INGRESS_VERIFIED=true only after a publicly reachable authorized ingress delivers a correctly signed Stripe test event to /api/billing/webhook. Current owner-private Site blocks unauthenticated webhook callers.
- BILLING_ENABLED=true only after ingress, provider test lifecycle, commercial offering, dispute/reversal handling and customer access are verified. Do not activate during this release; usage/gateway/spending and disputes remain incomplete.

Checkout defaults closed. Missing prerequisites return 503 without creating an order or calling Stripe. Successful checkout creation uses server-allowlisted pack and persisted price; owner/request uniqueness and Stripe idempotency key protect retries. Redirect alone never credits funds. Reconciliation retrieves the Session and checks paid/completed/mode/owner/currency/amount/live-mode before transactional unique ledger entry. Events supported: checkout.session.completed, checkout.session.async_payment_succeeded, charge.refunded. A known refund before original payment reconciliation returns a retryable failure. Disputes are NOT handled: implement and verify before activation. Timeout/orphaned session recovery and webhook operations should receive real provider failure testing.

## Launch acceptance still required
1. Real ChatGPT sign-in/onboarding, profile and cross-session stack/brief persistence; no fixture-only claims.
2. Intended public customer audience and reachable external API/webhook path verified without bypassing hosting controls.
3. Stripe test success/cancel/delayed event/duplicate/refund/outage tests; no actual purchase needed for QA. Verify paid customer who never returns is credited by webhook.
4. Dispute events, concurrent debit/spend protection, approved prices/taxes/refund policies before taking money.
5. Authorized upstream model access/resale terms, tenant gateway keys, rate limits, request accounting and margin controls. Catalog is discovery, not provisioned entitlement.
6. Mobile/responsive browser coverage and operational logs/health/support. Team membership/invites, shared billing, BYOK vault and retention/cache enforcement are future work; current controls state this plainly.

## Source attribution
Official source feed: https://openrouter.ai/api/v1/models . Initial complete feed: 430 entries, reported total_count 430 and next=null; snapshot metadata/source hash in data/models.json. Official API reference: https://openrouter.ai/docs/api/api-reference/models/list-all-models-and-their-properties . Catalog is refreshed explicitly by scripts/sync-models.mjs; no automatic live-refresh claim.
Stripe references: https://docs.stripe.com/api/checkout/sessions/create ; https://docs.stripe.com/webhooks/signature ; https://docs.stripe.com/checkout/fulfillment ; https://docs.stripe.com/api/idempotent_requests . These references informed implementation, not proof of this account being connected.

## Verification evidence
15 automated tests pass; tests execute actual TypeScript API modules with an isolated SQLite database using both migrations and mocked Stripe responses. No real Stripe credentials, payment, provider request or customer identity was used. Internal browser verifies public catalog/signup and anonymous console navigation. Private auth round-trip and mobile viewport remain unverified.
# 2026-09-26 — launch acceptance addendum

- Discovery and production are separate: the wider SubRouter catalog is informational until a model passes bounded identity, usage, receipt, cost, and response tests.
- API WILD remains the customer identity, payment, credit, key, reservation, debit, refund, and dispute authority.
- SubRouter is an upstream procurement/routing layer only. Its credential and wallet are never customer-facing.
- Customer onboarding is accepted only after an owner-controlled real email confirmation, onboarding save, local signout, fresh browser sign-in, profile persistence, and recovery flow succeed.
- Customer commerce is accepted only after one owner-controlled Stripe lifecycle proves payment, exactly-once credit, spend, refund/dispute handling, and provider-response/debit reconciliation.
- Failed or uncertain provider work never triggers an automatic retry that could double-charge. The reservation stays held for operator reconciliation.
