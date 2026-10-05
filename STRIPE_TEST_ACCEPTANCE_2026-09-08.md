## LIVE authorization and account readiness — 2026-09-08

The user now explicitly authorizes going live on Stripe; this supersedes the preceding TEST-only setup scope. Do not request the same activation approval again. Live account acct_1UCiHN194XZKj6cF / 2740797 ONTARIO INC. was verified using GetAccountsAccount: charges_enabled=true, payouts_enabled=true, details_submitted=true, card_payments=active; currently_due/past_due/pending_verification/errors empty and disabled_reason=null. Stripe account itself is already live.

API WILD connection remains incomplete: LIVE endpoint we_1UCyJf194XZKj6cFMlnobTtq is disabled at https://apiwild.com/api/billing/webhook (2026-08-26.dahlia); fresh prior application probe 503 Webhook not configured. Secure Site runtime settings inaccessible to editor; current Stripe dashboard login error Missing CAPTCHA response. No authenticated dashboard, new provider mutation or real charge. Existing sign-in must be completed without bypassing CAPTCHA; secrets belong only in authorized secure settings. Preserve production v19/a6d2b29, signup/password controls, branded Auth and deduplicated support. Canonical Stripe financial emails remain selected; unrelated disabled triggers, inference/API access and arbitrary real charges are not authorized.

Continuation: Resume GEN-10 from the LIVE-account checkpoint; read/update Linear first. Account is already charges/payouts enabled. Complete CAPTCHA/secure access, connect live credentials and matching existing endpoint secret, verify signed ingress and outstanding lifecycle checks, then finish already-authorized live integration. Do not fabricate acceptance or charge real money without transaction-specific authorization. Update exact evidence and finish with a fresh prompt.

# API WILD Stripe TEST acceptance — 2026-09-08

## Verified baseline before edits

1. Site/service: https://apiwild.com, existing public Site appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d, access revision 4; current connector caller is editor.
2. GitHub repository: historical audited export farhannabil/api-wild at 06d05055c7d5cb228287c857fecba6867eb4442e. Current GitHub parity is UNVERIFIED; organization preference GENXSTARK does not prove migration. Actual version 19 source is Sites-managed Git main, fetched and fast-forwarded without overwriting local changes.
3. Production commit: a6d2b29e53ff0aea18a06dbd94df3af1b9e13f94, version 19. Current work changes only sender policy, tests and handoff documents; no product deployment.
4. Linear issue: GEN-10, In Progress. Read issue/comments and wrote START CHECKPOINT 19ca7632-34bb-4ac1-a6f3-e6c9c24b2d11 before source changes.
5. Owner: Gen X Intel / contact@genxintel.com; Farhan Nabil is current editor.
6. Deployment evidence: appgdep_6aa00378b51c81919de7588d1e21620c; native succeeded, failure null, environment revision 6, updated 2026-09-08T12:48:00.698396+00:00. Saved version appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d~appgver_db976797b8d08191a97e88d41a68006e. Native latest version remains 19.

## Provider observations

- Only selected account: 2740797 ONTARIO INC. sandbox, acct_1UCiHk0SGcPsf6AA, livemode=false. No live account operation was performed.
- GetCheckoutSessions returned zero sessions, has_more=false. No API WILD checkout payment evidence exists in that result.
- Existing endpoint we_1UCzJN0SGcPsf6AAFAPXs6Wb points to https://apiwild.com/api/billing/webhook, status disabled, livemode=false, stage pending-ingress, API version 2026-08-26.dahlia. It includes checkout completion/async success/async failure/expiry, refund and dispute events. Left unchanged.
- GetPaymentIntents returned one unrelated Testing Blueprints CAD payment with no API WILD order metadata. It was not used, modified or refunded.
- Stripe operation discovery did not expose Checkout Session or PaymentIntent creation in this connection. Refund creation is exposed but there is no verified API WILD payment to refund.
- Sites secure environment getter returned NOT_FOUND/project_not_found. This is an access limitation, not evidence that runtime variables are absent. No alternate settings-write path was attempted.
- Earlier browser session did not survive. Secure browserAuth sign-in was submitted using the user-selected email/password method. Stripe then rendered an image-based hCaptcha challenge; no signed-in dashboard evidence exists. No CAPTCHA was attempted or bypassed. Native receipt/invoice/refund email settings and branding have not been observed. Next step is user completion of that challenge or explicit authorization to attempt solving it in the current browser.

## Sender selection

See emails/transactional/manifest.json and README.md for the explicit ownership mapping. Stripe native owns one financial-success paid-invoice summary with invoice and receipt links, and each successful refund notice. Custom payment-received, invoice-ready and refund-confirmed stay suppressed; no automatic fallback. Supabase Auth via Resend SMTP remains the Auth sender. Existing support-inbound via Resend remains support acknowledgement sender. API WILD via Resend is selected for the remaining business events, all disabled. This is a policy selection, not an activated sender or proven delivery pipeline.

Official Stripe receipts documentation checked 2026-09-08: https://docs.stripe.com/receipts . Test receipts require a manual send. Paid invoice summaries can include both invoice and receipt links. Manual test email evidence must not be described as automatic live acceptance.

## Validation matrix

| Scenario | Local application evidence | Real Stripe / delivery evidence |
| --- | --- | --- |
| Checkout, server price, verified recipient, retries | PASS existing handler fixtures | OPEN: zero Checkout sessions; test configuration/creation access needed |
| Receipt ownership and invoice request | PASS fixtures and canonical-sender guard | OPEN: native settings, paid invoice and inbox delivery unverified |
| Terminal async failure | PASS signed-event test: one event, failed order, zero credits; late failure cannot undo verified payment | OPEN: actual sandbox failure not executed |
| Cancellation / expiry | PASS expiry yields expired order and no credits | OPEN: actual Checkout abandonment not executed |
| Partial refund | PASS signed-event test: 2500 to 1500 cents; duplicate and related charge event cause no extra debit | OPEN: actual sandbox refund not executed |
| Full refund | PASS signed-event test: remaining 1500 refunded, balance zero, exactly three ledger rows | OPEN: actual sandbox refund not executed |
| Pending / failed refund | PASS no credit reversal | OPEN: actual provider status test not executed |
| No-return payment reconciliation | PASS signed webhook commits once without any return call; replay and DB retry safe | OPEN: disabled provider endpoint; no signed production delivery |
| Taxed refunds, auth isolation, mode separation, support dedup, branded templates | PASS existing regression suite | Prior Auth/support evidence preserved; not re-sent |

Production build and all 49 automated tests passed with zero failures/skips. These tests use isolated SQLite and mocked provider responses. No test claims a real Stripe payment, public D1 reconciliation, email delivery, inference, or usable API entitlement.

Production /signup returned 200 with API WILD branding and Show password control; anonymous /api/billing returned 401. An unsigned empty webhook probe returned 503 with `Webhook not configured.`; it could not process an event or modify the ledger. This independently confirms ingress is not ready without exposing runtime values. Signup celebration, password controls, Auth templates, support worker and its active trigger were untouched.

## Owned blockers and next atomic action

Owner: Gen X Intel / Farhan Nabil. Complete secure Stripe dashboard sign-in to the existing sandbox, inspect native customer-email settings, and make sandbox-only key plus matching existing webhook secret available through authorized owner settings. Do not paste secrets into chat. Native Sites settings access remains unavailable to this editor; resolve through owner/platform support, not an alternate API.

Then verify signed test ingress before asserting WEBHOOK_INGRESS_VERIFIED, run owner-controlled test Checkout, confirm exactly one credit without a browser return, perform decline/terminal failure and partial/full refund cases, and record provider IDs, D1 rows and inbox counts. Do not mutate unrelated sandbox payments. Do not enable live billing/payments/inference/API access, COMMERCE_READY, or disabled business-email triggers. Test checkout authorization does not authorize customer email-trigger activation or live launch. Keep production v19 and its existing auth/support behavior intact.

## Continuation prompt

Resume API WILD GEN-10 from the latest 2026-09-08 Stripe TEST acceptance checkpoint. Read/update Linear first and read STRIPE_TEST_ACCEPTANCE_2026-09-08.md, HANDOFF.md and AGENTS.md. Production is verified v19/a6d2b29e53ff0aea18a06dbd94df3af1b9e13f94; subsequent policy/test source is not a deployment. Preserve signup celebration, password controls, branded Auth emails and deduplicated support acknowledgement. Use only sandbox acct_1UCiHk0SGcPsf6AA. Resolve secure dashboard/runtime-setting access, reuse disabled endpoint we_1UCzJN0SGcPsf6AAFAPXs6Wb, verify signed ingress and actual Checkout/receipt/invoice/terminal failure/partial/full refund/no-return cases. The 49 passing local tests are fixtures, not provider acceptance. Stripe is canonical for financial receipt/invoice/refund messages; custom alternatives and all other disabled business triggers remain off. No live billing, payments, inference or API access without explicit approval and evidence. Update Linear with exact results and finish with a fresh continuation prompt.
