# API WILD Stripe integration and activation

State: implemented for prepaid USD credit packs; provider acceptance and production activation remain OPEN. This is not an inference/spend gateway or recurring subscription product. Existing packs are $25, $100, $250 before applicable tax.

## Implemented

- Supabase bearer-token verification on the server, confirmed email and completed onboarding before purchase. No identity headers or customer IDs accepted from the client.
- Test/live-separated customer mappings and wallet owners. Existing legacy balances are intentionally not silently assigned to Supabase accounts; an owner-verified migration is required if legacy balances exist.
- Stripe-hosted checkout with dynamic payment methods, 3DS handled by Stripe, collected billing address/tax ID, optional automatic tax, paid invoices, server-priced packs, durable checkout/customer idempotency, atomic checkout rate limit.
- Durable webhook receipts; raw-body timestamped HMAC validation; duplicate events, provider mode, order ID, amount, currency and fulfillment verification; credits committed atomically with payment state. Return-page verification is an additional recovery path, never the only fulfillment path.
- Successful cumulative refund accounting, including proportional credit reversal for tax-inclusive payment refunds. Old snapshots cannot restore refunded credit. Refund failure events do not reverse credit. More than 100 refunds on one payment requires operator review; webhook remains retryable.
- Latest Stripe dispute retrieval, bounded credit holds for needs_response/under_review/lost, automatic hold release on won, terminal outcomes protected against stale events. Warnings do not remove funds. Dispute fees are operator expenses, not customer wallet debits.
- Customer billing UI, history, owner-scoped Stripe receipts, configured customer portal, disabled/loading/error/cancel/pending/success states. No card details stored by API WILD.

## Server configuration (never place secrets in client code or chat)

| Setting | Purpose |
| --- | --- |
| SUPABASE_URL / SUPABASE_PUBLISHABLE_KEY | Existing API WILD Supabase project, verifies the customer's access token and profile through RLS |
| STRIPE_SECRET_KEY | Matching Stripe test or live server key, securely configured by the Site owner |
| STRIPE_WEBHOOK_SECRET | Signing secret for this exact endpoint and account mode |
| SITE_ORIGIN | https://apiwild.com (HTTPS origin without trailing slash) |
| STRIPE_PORTAL_CONFIGURATION_ID | Matching-mode billing portal configuration, with billing details/payment-method updates and invoice history enabled |
| STRIPE_AUTOMATIC_TAX | true only after Stripe Tax settings, product tax treatment and applicable registrations are configured |
| BILLING_ENABLED | true to open checkout after acceptance gates below |
| WEBHOOK_INGRESS_VERIFIED | true only after a real signed provider delivery reaches this deployment and commits once |
| COMMERCE_READY | Required true for live checkout only after the owner verifies commercial policies, available service, spend enforcement and launch approval |

API calls pin Stripe API 2026-08-26.dahlia. Register snapshot events at the same API version. Checkout disables adaptive currency conversion because the wallet is denominated in USD, and uses a stable integration identifier for Dashboard analytics. Checkout generates product/price data server-side; no manual product/price IDs are required.

## Webhook registration

Endpoint: https://apiwild.com/api/billing/webhook

Events:

- checkout.session.completed
- checkout.session.async_payment_succeeded
- checkout.session.async_payment_failed
- checkout.session.expired
- charge.refunded
- refund.created
- refund.updated
- refund.failed
- charge.dispute.created
- charge.dispute.updated
- charge.dispute.closed
- charge.dispute.funds_withdrawn
- charge.dispute.funds_reinstated

This endpoint must bypass customer sign-in through the public Site dispatcher, using Stripe signature verification as its sole authentication. Never change whole-Site access merely to probe ingress. Failed processing returns 503, logs event ID/status only, and does not mark the event processed. Stripe delivery history is the operational retry queue; monitor failures and replay the same event after fixing the cause. Keep the webhook operating even when checkout is disabled so already-paid orders/refunds continue to reconcile.

## Test acceptance, then live launch

1. Deploy the saved integration including immutable D1 migration 0002_careful_medusa.sql to the intended Site. Leave billing disabled initially. No Supabase schema migration is required.
2. Use the connected Stripe account to verify correct business identity and mode. Configure test credentials, portal, endpoint and any tax settings through secure owner-accessible settings. Confirm raw signed delivery reaches the endpoint.
3. Set test-only checkout flags. Using an owner-controlled verified customer, test successful card purchase, 3DS, decline, cancellation, retry, expired session, and payment where the browser never returns. Check one ledger credit for duplicate/concurrent events.
4. Test partial/full and tax-bearing refunds, refund before fulfillment, delayed/duplicate events, dispute hold and won/lost resolution. Verify account isolation, test/live isolation, portal invoices and receipts. Reconcile Stripe payments/refunds with D1 orders/ledger. Local fixture tests are not this evidence.
5. Owner must confirm activated Stripe business, charges/payout capabilities, business/contact branding, statement descriptor, bank/payout details, receipt settings, fraud controls, tax treatment/registrations, customer purchase/refund/privacy terms and support ownership. Existing site terms describe planning only and need owner-approved purchase terms before COMMERCE_READY.
6. Separately verify usable paid API service and atomic spend enforcement. The current catalog alone is not a paid service. Do not enable real credit sales merely because Stripe works.
7. Configure separate live keys/endpoint/portal and verify live-mode ingress. Enable COMMERCE_READY and checkout only after recorded launch acceptance. A real transaction or refund must be explicitly authorized; don't charge a saved card as a test.

## Operational recovery

- Disable BILLING_ENABLED to stop new purchases; retain secrets/webhook for existing payment reconciliation.
- Failed session creation can reuse its persisted request ID within 23 hours. Older ambiguous customer-creation records require an operator to locate the Stripe customer by metadata and repair its mapping before retrying. Never blindly create duplicate customers.
- Review billing.webhook_failed in worker logs and Stripe delivery failures. Inspect event and payment in Stripe; replay only after correcting the issue. Do not manually mark events received or fabricate credits.
- Refund from Stripe Dashboard (or authorized connector action), then verify wallet reversal. Refunds do not automatically authorize a support message.
- Balance holds are exposed in billing and must be enforced by any future metered API spend function. That spend function is not implemented by this payment integration.

## Current access and provenance checkpoint — 2026-09-07

1. Site/service: API WILD https://apiwild.com; appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d, public; current role editor.
2. GitHub repository: farhannabil/api-wild linkage MISSING/UNVERIFIED. Actual editable source is Sites-managed Git main; do not equate them.
3. Production commit: 00ab4e610400b4011b357f5070671a7336189e54, version 13. This new integration is not yet deployed.
4. Linear issue: GEN-10, https://linear.app/genxintel/issue/GEN-10/build-ai-model-api-resale-platform. Read issue, recent comments and handoff protocol. Outgoing checkpoint deferred under current session communication restriction.
5. Owner: Gen X Intel/contact@genxintel.com; editor Farhan Nabil. Owner owns secure runtime-setting access and launch acceptance.
6. Deployment evidence: prior succeeded appgdep_6a9e699c1fa881918b8017bc1d7fb3e1. No new production deployment or real Stripe charge is claimed.

Stripe connection is confirmed by the user's connection event. The running tool registry still exposes zero Stripe account actions after refresh/discovery; no account capability, key, webhook or portal setting has been read or changed. Do not ask the user to reconnect. Continue with the already-connected Stripe plugin when its tools are exposed in the next session.

Sites get_environment_variables returned NOT_FOUND for this editor despite successful Site and source access; do not infer credentials absent. Owner-side secure setting access is required, without requesting secret values in chat.

## Stripe integration saved — 2026-09-07

Implemented Supabase-authenticated Stripe billing, test/live isolation, server-priced checkout, invoices, customer portal, receipts, durable webhook deduplication, tax-aware refunds, dispute holds and customer billing UI. Validation: all 32 automated tests pass, TypeScript passes, production build passes; archive includes new D1 migration. No real Stripe transaction or browser payment test occurred.

1. Site/service → API WILD https://apiwild.com, same existing public Site.
2. GitHub repository → farhannabil/api-wild source linkage MISSING/UNVERIFIED; actual source is Sites-managed Git main.
3. Production commit → unchanged 00ab4e610400b4011b357f5070671a7336189e54, version 13. New pushed integration a470be5e30f05d1a9e4667586506e9f34b0e3b49 is saved as version 14, NOT deployed.
4. Linear issue → GEN-10; issue/recent comments/protocol read. Outgoing update deferred under current session communication restriction; checkpoint retained here.
5. Owner → Gen X Intel/contact@genxintel.com; editor Farhan Nabil. Owner owns provider settings and production acceptance.
6. Deployment evidence → existing succeeded appgdep_6a9e699c1fa881918b8017bc1d7fb3e1. New saved version appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d~appgver_42544b1c5d4c819181eeadb538d8e293, archive sha256:fa5cff21ace60027bb69a7585109c088274dc0e91ef15ed70ac4503dd7ce80e4. Saving is not deployment.

Blockers: Stripe connection CONFIRMED by user; tools still absent from this running registry after discovery, so no Stripe account/keys/webhooks/portal configuration was read or changed. Do not ask to reconnect. Sites runtime-settings read returned NOT_FOUND despite Site/source access; owner must make secure runtime setting access available. No secret requested in chat. Billing activation remains unverified/disabled by application gates; commercial terms still describe planning and usable metered service remains a live-sales prerequisite.

Next: use the already-connected Stripe tools in a refreshed session; verify correct account and test mode, configure test credentials/endpoint/portal through secure owner settings; publish saved integration only when requested; perform actual checkout/webhook/refund/portal acceptance. Live launch additionally needs approved commercial terms, tax/account capability checks and usable spend-controlled service. See STRIPE_PRODUCTION.md for exact settings, events and release gates. Preserve concurrent SMTP/template changes, which are excluded from this integration commit and saved archive.

Continuation: Resume API WILD GEN-10 Stripe integration from saved version 14 in /workspace/sites/api-wild. Keep current production version 13 distinct from saved code. Stripe is already connected; finish secure provider configuration, prove payment and refund lifecycle, then complete authorized release. Preserve auth/email work and update provenance.


## Stripe setup resumed — 2026-09-07

Verified saved version 14 exists. Stripe skills are loaded but no Stripe MCP account tools are exposed. Site settings read still returns NOT_FOUND while get_site confirms editor access. Installed official Stripe CLI 1.50.10 through npm exec; whoami confirms not authenticated, with no test/live keys. The supported non-interactive pairing login is the next action, without asking for a secret in chat.

Updated request API version to current stable 2026-08-26.dahlia (official changelog), enabled dynamic payment-method selection, added a stable Checkout integration identifier, and disabled automatic currency conversion to preserve the USD wallet's verification/accounting contract. Checkout fixtures now verify those settings; 17 lifecycle tests pass. No provider settings or live payments changed. Existing account/email edits remain untouched.

Provenance: API WILD → GitHub farhannabil/api-wild mapping unverified (Sites Git actual source) → production 00ab4e610400b4011b357f5070671a7336189e54/v13 → GEN-10 → Gen X Intel → previous succeeded appgdep_6a9e699c1fa881918b8017bc1d7fb3e1; next saved integration pending. Outgoing Linear update deferred under current session communication restriction.


## Stripe version 15 saved — 2026-09-07

Lifecycle regression tests: 17/17 pass. TypeScript and production build pass. Saved (not deployed) version 15: appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d~appgver_b06dee72a3608191ac3e9ff6e8891367; source 27144df0eec2488f40803c483bcea1069f67d5b8; archive sha256:f8da7752725e120733f19aebe87c02e359866a56e9693d7171837ee99d433079. This includes previously committed email-template work without modifying it.

Code changes: Stripe API 2026-08-26.dahlia; dynamic payment methods; fixed USD checkout currency; stable integration identifier. Live production remains v13/00ab4e610400b4011b357f5070671a7336189e54. Stripe CLI 1.50.10 is available through npm exec; whoami is unauthenticated. Secure non-interactive pairing login has been started; no credential contents read or stored in this repository. Poll the existing login session before creating another. Site runtime-settings read still fails NOT_FOUND for current editor. No provider mutation, payment, tax activation or production deployment claimed.

Provenance: API WILD → GitHub mapping unverified (Sites Git actual source) → live production commit above → GEN-10 → Gen X Intel/contact@genxintel.com → existing succeeded deployment appgdep_6a9e699c1fa881918b8017bc1d7fb3e1; v15 saved only. Continue with secure Stripe pairing, test-account verification, owner-authorized runtime settings, and actual payment/refund testing.


## Stripe account connected and live configuration prepared — 2026-09-07

Verified official Stripe CLI OAuth authorization for 2740797 ONTARIO INC., acct_1UCiHN194XZKj6cF. Authorized scope currently includes LIVE mode only, no sandbox/test context. Account charges_enabled=true, payouts_enabled=true, details_submitted=true; requirements currently_due/past_due/errors empty. Statement descriptor is API WILD. Business website remains genxintel.com; global business profile/branding and payout settings were not modified. No tax registrations exist; automatic tax must remain disabled pending verified setup. Customer sender requirements remain an apiwild.com domain; no receipt email sender has been verified or changed here.

Created and READ-BACK VERIFIED live portal configuration bpc_1UCyHn194XZKj6cFkKN0vwa7: API WILD customer billing; headline Manage your API WILD billing; return URL https://apiwild.com/console/billing; invoices, payment-method updates and customer email/address/name/phone/tax-ID updates enabled; subscriptions and shareable portal login disabled. An interrupted tool-result retrieval reported network approval cancellation, but read-only reconciliation confirmed creation succeeded; no duplicate creation attempted.

Created live webhook we_1UCyJf194XZKj6cFMlnobTtq at https://apiwild.com/api/billing/webhook, pinned 2026-08-26.dahlia, subscribed to the 13 documented checkout/refund/dispute events. Immediately disabled it and verified status=disabled. Signing secret retained only in ephemeral task state, never in source or user-facing output; the Site does NOT have this secret configured. If ephemeral state is lost, owner can retrieve it securely from Stripe. Endpoint was not tested and must remain disabled pending deployment, configured secret and signed ingress proof.

Site environment reads AND the attempted SITE_ORIGIN write returned NOT_FOUND for the current editor. No runtime values changed. Owner Gen X Intel/contact@genxintel.com must open/configure secure Site settings or resolve this access failure; do not bypass it using a different backend. Runtime still needs restricted Stripe key, this signing secret, portal ID and test-first activation flags. No live charges/refunds initiated, no new customer records, no payment activation and no new deployment.

CLI reauth started to add sandbox/test authorization and is waiting for the user. Reuse the existing reauth process; do not start another pairing. After approval, run whoami to verify contexts and select an authorized sandbox before test requests. Current live context must not be used for payment fixtures. Keep secrets and authorization URLs out of this repository.

Provenance: API WILD https://apiwild.com → GitHub farhannabil/api-wild linkage UNVERIFIED, Sites-managed Git actual source → production 00ab4e610400b4011b357f5070671a7336189e54/v13 → GEN-10 → Gen X Intel/contact@genxintel.com → existing succeeded appgdep_6a9e699c1fa881918b8017bc1d7fb3e1. Saved v15 appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d~appgver_b06dee72a3608191ac3e9ff6e8891367/source 27144df0eec2488f40803c483bcea1069f67d5b8 is NOT deployed. Outgoing Linear checkpoint deferred under session communication restriction; provider evidence retained here.

Continuation: Resume API WILD Stripe setup from saved v15. Live account is verified, portal created and webhook created/disabled. Complete existing sandbox authorization; solve Site owner runtime-settings access; configure test credentials and matching test portal/webhook; deploy only within publishing authorization and prove checkout, delayed/duplicate events, refunds, portal and receipts before live activation. Preserve concurrent apiwild.com email sender work.


## Sandbox authorization verified and webhook prepared — 2026-09-07

This checkpoint supersedes earlier statements that Stripe tools or sandbox access are unavailable. Native Stripe account discovery confirms sandbox acct_1UCiHk0SGcPsf6AA (2740797 ONTARIO INC. sandbox, livemode=false) and live acct_1UCiHN194XZKj6cF. Sandbox Checkout Sessions, portal configurations and webhook endpoint lists were initially empty. Accepted the existing hosted Checkout implementation plan iguide_61VMNC0x0pkhPAJ95410SGcPsf6AA; no architecture change required.

Created sandbox webhook we_1UCzJN0SGcPsf6AAFAPXs6Wb at https://apiwild.com/api/billing/webhook, API 2026-08-26.dahlia, with all 13 documented events. Immediately disabled it; a separate retrieval verifies livemode=false and status=disabled. Signing secret remains only in ephemeral task state and must be transferred through secure Site settings; never request it in chat or store it in source. Existing live webhook remains disabled. No payment, refund, customer creation, runtime configuration change, or deployment occurred.

Remaining access findings: CLI whoami still exposes live only; selecting the sandbox returns "not found in your authorized accounts". No further pairing started and no credential-file workaround attempted. Native sandbox tools work for webhook writes, but API search exposes only reads for Checkout Sessions, PaymentIntents and portal configurations, so exact application payment tests cannot be completed through those operations. The account-info tool itself returns Unknown tool; account selection is grounded in the successful account-list response instead.

OWNER ACTION — Gen X Intel/contact@genxintel.com: restore access to API WILD secure environment settings (native reads still return NOT_FOUND despite working Site/source access). Configure the sandbox restricted key, matching webhook secret and sandbox portal through owner-accessible secure settings. This blocks deployed checkout, signed ingress and payment/refund acceptance. Interim state: saved integration v15 is not deployed; new sandbox and live webhooks are disabled; live sales are not activated. Closing verification: successful secure-setting access, correct sandbox runtime mode, authorized deployment of v15, signed delivery, then actual successful/declined/3DS/cancelled checkout, duplicate delivery, refund, portal and receipt checks. Local test fixtures do not close this gate. Live launch additionally needs usable paid API service/spend enforcement and owner commercial/tax/branding acceptance.

Provenance: API WILD https://apiwild.com → GitHub farhannabil/api-wild linkage UNVERIFIED (Sites-managed Git is actual source; verify repository mapping) → production 00ab4e610400b4011b357f5070671a7336189e54/v13 → Linear GEN-10 → Gen X Intel/contact@genxintel.com → succeeded deployment appgdep_6a9e699c1fa881918b8017bc1d7fb3e1. Saved v15 source 27144df0eec2488f40803c483bcea1069f67d5b8 remains undeployed. No new source release for this evidence-only checkpoint. Outgoing Linear update deferred under session communication restriction.

Continuation: Continue API WILD Stripe from saved v15. Sandbox access is verified and webhook we_1UCzJN0SGcPsf6AAFAPXs6Wb is created/disabled. Resolve owner secure-settings access, configure sandbox key/secret/portal, then complete authorized deployment and real sandbox lifecycle verification. Preserve concurrent apiwild.com email work.


## Stripe v15 deployed at explicit user request — 2026-09-07 10:01 UTC

User explicitly requested immediate live deployment. Reused the verified archive-backed saved v15, without rebuilding or including dirty concurrent documentation. Native deploy and same-ID status confirm SUCCEEDED: appgdep_6a9e8b64e3f081918db95e5646c5d6f9, environment revision 2, saved version appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d~appgver_b06dee72a3608191ac3e9ff6e8891367, exact source 27144df0eec2488f40803c483bcea1069f67d5b8. Returned deployed URL: https://legacy-ai-exchange.genxintel-6787.chatgpt.site. Site lookup confirms existing public audience and custom URL https://apiwild.com. This supersedes older statements that production remains v13 or v15 is undeployed.

Payment activation is NOT complete. Native secure-settings read and runtime-log read still return NOT_FOUND for current editor, despite successful Site/version/deploy operations. No runtime values changed. Sandbox/live webhooks remain disabled. Agent HTTP checks against custom-domain /api/billing, /api/billing/checkout and /api/billing/webhook all return edge HTTP 403/code 1010; these do not prove application responses or imply every customer is blocked. Do not bypass the edge access check or substitute those responses for signed Stripe delivery evidence. No payment/refund or authenticated billing acceptance completed.

Owner: Gen X Intel/contact@genxintel.com must open this same Site under the owner account and restore native secure-settings access, or escalate the inconsistent Sites project-not-found error to platform support. Configure the sandbox key, matching webhook secret and portal through secure settings; never paste keys in chat. Closing verification requires accessible runtime settings/logs and genuine signed ingress, then sandbox checkout/refund/portal acceptance before live checkout activation. Production code is published; money movement readiness remains blocked.

Provenance: API WILD https://apiwild.com → GitHub farhannabil/api-wild linkage UNVERIFIED (verify mapping; actual source is Sites-managed Git) → deployed source 27144df0eec2488f40803c483bcea1069f67d5b8/v15 → Linear GEN-10 → Gen X Intel/contact@genxintel.com → succeeded deployment appgdep_6a9e8b64e3f081918db95e5646c5d6f9. Outgoing Linear checkpoint remains deferred under session communication restriction.

Continuation: Continue API WILD Stripe activation. V15 is now deployed; do not redeploy it unnecessarily. Resolve owner secure-settings/log access and signed webhook ingress, configure sandbox credentials securely, complete payment/refund/portal tests, then finish live activation prerequisites. Preserve apiwild.com email work.


## Stripe activation recheck — 2026-09-07 12:52 UTC

Confirmed newest website release v17 is deployed successfully, source1453f3cd896ea18b29ebb141c73437e79ea9467b, deploymentappgdep_6a9e980bc40c819196f214f6401ff180. Preserve email/support updates; do not restore/redeploy v15. Native secure-settings read STILL returns NOT_FOUND and current user role remains editor. Stripe sandbox/live account discovery succeeds. No runtime values or provider payment activation changed; payment/refund acceptance remains incomplete.

Owner action remains Gen X Intel/contact@genxintel.com: resume from the owning ChatGPT account and verify secure-settings access; if the same native error persists there, platform support must resolve it. Do not work around the access failure with another backend or ask for secrets in chat. Deployment success does not close credential or signed-ingress gates.

Provenance: https://apiwild.com → intended GitHub farhannabil/api-wild (previous access blocked; no new GitHub verification) → deployed1453f3cd896ea18b29ebb141c73437e79ea9467b/v17 → Linear GEN-10 (outgoing update deferred) → Gen X Intel/contact@genxintel.com → native succeeded appgdep_6a9e980bc40c819196f214f6401ff180. Continuation: Continue API WILD Stripe activation from owner account; preserve live v17 and support automation, resolve secure settings, then complete real sandbox acceptance before live payments.


## Owner browser settings access RESOLVED — 2026-09-07

User signed into the owner browser and explicitly requested browser completion. Opened the actual API WILD settings page through Sites list > More actions > Settings: https://chatgpt.com/sites/appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d/settings. The owner UI exposes editable environment variables; native connector still returns NOT_FOUND because browser authentication does not change this chat's connector identity. Do not ask the owner to log in again or claim all settings access is blocked.

Saved and reload-verified SITE_ORIGIN=https://apiwild.com, BILLING_ENABLED=false, WEBHOOK_INGRESS_VERIFIED=false, COMMERCE_READY=false and STRIPE_AUTOMATIC_TAX=false. Preserved existing BAIDU secret and Supabase settings. No Stripe server key/webhook secret is installed yet. Prior ephemeral webhook secret is unavailable; retrieve the existing sandbox endpoint's secret securely through Stripe Dashboard. Changes require deployment to apply; do not redeploy until the remaining sandbox configuration is ready.

Opened Stripe Dashboard login. Secure browserAuth accepted user-selected email/password submission, but Stripe rendered "Missing CAPTCHA response. Try again." No authenticated Stripe browser session is proven. The next action is manual user completion of Stripe verification in the existing dashboard.stripe.com/login tab; do not inspect credentials, change login methods, bypass the challenge or restart account pairing. After sign-in, configure restricted sandbox key, matching webhook secret and sandbox portal, then deploy existing latest release with updated runtime configuration and perform genuine Stripe lifecycle checks.

Provenance: API WILD https://apiwild.com → intended GitHub farhannabil/api-wild (no new linkage verification) → last verified website1453f3cd896ea18b29ebb141c73437e79ea9467b/v17 → Linear GEN-10 (outgoing update deferred) → Gen X Intel/contact@genxintel.com owner browser → succeeded website deploymentappgdep_6a9e980bc40c819196f214f6401ff180; no new deployment/payment activation this checkpoint.

Continuation: Owner Site settings access is resolved. Finish existing Stripe browser CAPTCHA/login; configure restricted sandbox key, existing webhook secret and matching portal in the owner Site settings; apply runtime changes and verify real sandbox payments/refunds before live activation. Preserve email/support and GitHub work.

