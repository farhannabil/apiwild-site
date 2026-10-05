# Production review — 2026-09-08

Scope: user-authorized live Stripe connection and complete production/customer-flow regression from source checkpoint `5540b1050ef082c2d9011400d74dbd6ea0d826ef`. Deadline stated as September 8 noon Montréal (`America/Toronto`), 16:00 UTC. Four parallel read-only audits covered payments, auth/support, architecture, and CI/cron; the parent integrated and tested all changes. The latest user explicitly requested completion in this run and no continuation prompt.

## Released result

Sites **version 20** deployed from `841254ad40ceb1eb5545f7ca0b374bce7cd7c4e4`: deployment `appgdep_6aa01eaa8a3c8191ad6d03fd280b752a` succeeded September 8 at 14:42:01.787792 UTC, environment revision 6. Support receiver **version 5** is ACTIVE; all three deployed files match source exactly, with index/template and signature/dedup behavior preserved.

Post-release: 11 routine HTTP checks and 30 additional public routes/access-boundary checks passed; oversized unsigned support body returns 413. App Stripe webhook still returns 503 “Webhook not configured.” No real payment or inbox acceptance is claimed.

GitHub draft PR 1 now contains public-source commit `4e0931c4a2daa2421a21f2634ee756bff204a89a`, with exact hashes for all 33 exported files. Its current CI run [34240101119](https://github.com/farhannabil/api-wild/actions/runs/34240101119) failed before build steps (job `102107759785`, 14:43:28–14:43:30 UTC); production-health correctly skipped for the PR event. Four observed runs now, zero successes. Main was not merged and the workflow still does not deploy Sites. Private checkpoints and secure config were not exported.

The public discovery/account maintenance release is deployed. The requested full paid API-service launch remains blocked by the open gates below.

## Provenance before edits

1. Site/service: https://apiwild.com; Site `appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d`. Separate Supabase support receiver on project `yautmilnpllojugpmfgy`.
2. GitHub: `farhannabil/api-wild`, main `06d05055c7d5cb228287c857fecba6867eb4442e`; existing draft PR 1 initially `93d63a1ad3db3015a742cf8621eeed0d23380411`. This is an export, separate from Sites-managed source.
3. Production commit: `a6d2b29e53ff0aea18a06dbd94df3af1b9e13f94`, version 19, natively verified succeeded before editing.
4. Linear: GEN-10, https://linear.app/genxintel/issue/GEN-10/build-ai-model-api-resale-platform. Read and updated before product edits.
5. Owner: Gen X Intel; connected editor Farhan Nabil. Current verified GitHub identity `farhannabil`; installed organization `wolvesfield`. An alternate designated destination is unverified.
6. Deployment evidence: `appgdep_6aa00378b51c81919de7588d1e21620c`, environment revision 6, public audience revision 4. Follow-up deployment result belongs in DEPLOYMENT_EVIDENCE.md.

## Implemented architecture and scope

| Component | Actual path | Acceptance status |
| --- | --- | --- |
| Discovery | React/vinext → Worker → catalog snapshot, 581 models | Public pages and browser search/filter/details work. Listings are reference data. |
| Customer auth/profile | Supabase Auth → RLS-owned customer_profiles | Existing signup/confirmation/recovery and profile flow preserved. New identity-switch and malformed-data regressions covered locally. New real inbox/session acceptance was not performed. |
| Prepaid billing | Verified Supabase user → test/live separated D1 owner → Stripe Checkout; signed events → atomic ledger/refunds/disputes | 24 payment/lifecycle fixtures pass. Real API WILD Checkout, receipts/invoices, terminal failure, partial/full refund and no-return signed delivery remain unverified. |
| Legacy planning | Static workspace → Sites identity → D1 | Working legacy paths preserved. Public 401 now offers downloads; does not promise Supabase sign-in enables legacy persistence. |
| API service | Existing `/v1/models` and `/v1/usage` read-only handlers | No inference handler, usage-writing path, spend reservation/debit, or provider runtime acceptance. Six customer-console sections inactive. Paid API-service launch remains incomplete. |
| Support | Supabase Edge Function → signed Resend event → database claim/lease → idempotent acknowledgement | v4 source parity verified before edit. Bounded body-read fix tested; template/index and dedup behavior preserved. Provider deployment tracked separately. |
| Operations | GitHub scheduled CI/health + Supabase daily cron + existing daily maintenance task | Database cron succeeded today. All observed GitHub runs failed before steps; no successful CI or GitHub-to-Sites CD exists. |

## Fixes reviewed and integrated

- Billing refresh clears only the matching finished checkout request, so a paid customer who never returns can buy the same pack again. Open/unrelated attempts remain intact.
- Webhooks acknowledge unrelated Stripe products carrying generic `order_id` metadata. Persisted API WILD orders remain retryable while session/payment linkage completes.
- Reconciliation returns durable paid/partial-refund/full-refund status; reopening refunded checkout shows an accurate balance message and cannot re-credit funds.
- Profile saves pin the loaded owner; cross-tab account changes clear stale data. Stored JSON is normalized field by field to prevent crashes while recovering valid data.
- Support request streaming stops at the 64KiB limit before signature verification, handles split UTF-8 and read failures, and preserves all claim/send/dedup logic.
- Public planning 401 responses show working download guidance; successful legacy saves and temporary retry paths are retained.
- Recovered exact already-applied customer-profile migrations `20260907010505`, `20260907010527`, and corrected the expansion filename to actual applied `20260907013634`. Source recovery only; no SQL replay or live schema change.
- Removed stale 430-model copy and corrected the limited scope of scheduled checks. Updated the existing maintenance task to current authority without creating another schedule.

## Verification

- All **64 source regression tests passed**, including auth callbacks, tenant isolation, profile/stack persistence, key lifecycle, credit idempotency, webhook signatures/modes/races, terminal failures, taxed partial/full refunds, dispute holds, canonical senders, support suppression/dedup, and SPF resolution.
- TypeScript: zero diagnostics with `--noEmit --incremental false`.
- Sites production build: succeeded. Existing bundle-size warning remains; no build failure. Build performed with local public-preview configuration removed.
- Browser on supported local preview: signup/login password visibility; recovery links and expired-token message; signed-out onboarding/billing redirect to login; catalog search, filter and details; planning add-to-stack, denied-account guidance, and download action showing “Download prepared. No data was submitted.”
- Pre-release production checks: all 11 HTTP page/auth/catalog/support checks passed. Local native DNS resolver returned ECONNREFUSED; independent public DNS-over-HTTPS checks passed all five MX/SPF/DKIM/DMARC checks at 14:37:47–14:37:48 UTC. This establishes records, not inbox delivery.
- Supabase support daily job 1, `17 13 * * *`, active: run 2 succeeded September 8 13:17:00.163930–13:17:00.192551 UTC. Last-24h metrics zero sent/suppressed/review/stale; lifetime sent 1, processing 0, expired 0. No new support email was sent.
- Existing daily maintenance task `6a9ea5c2b7dc8191af3bb72293786d0c` updated and enabled; schedule preserved. Task execution is distinct from successful GitHub CI and from payment monitoring.

## Canonical customer email ownership

| Event | Canonical sender | Active state |
| --- | --- | --- |
| Auth confirmation/recovery/change | Supabase Auth via branded Resend SMTP | Existing configuration preserved |
| Paid invoice with receipt/invoice links | Stripe native single paid-invoice summary | Selected in policy; provider configuration/delivery unverified |
| Successful partial/full refund | Stripe native per successful refund ID | Selected in policy; provider configuration/delivery unverified |
| Initial support email | Existing support-inbound via Resend | Active; idempotent acknowledgement preserved |
| Other business events | Manifest-designated sender | Ten custom business triggers remain disabled; no new activation |

Custom payment-received/invoice-ready/refund-confirmed templates remain suppressed with no fallback sender. Tests verify a single owner per financial-success group.

## Open gates with owners and closing evidence

| Gate | Owner and exact missing item | Current state and closing verification |
| --- | --- | --- |
| Application Stripe connection | Gen X Intel/Farhan: complete existing Stripe security challenge and provide authorized access to Site secure runtime settings | Live account `acct_1UCiHN194XZKj6cF` already has charges/payouts enabled and active card payments. Live endpoint `we_1UCyJf194XZKj6cFMlnobTtq` disabled; application webhook returned 503 unconfigured. Runtime getter denies this editor (`NOT_FOUND`). No bypass or credential exposure. Close with secure configured endpoint, real TEST lifecycle/inbox acceptance and then authorized live ingress. |
| Paid service availability | API WILD engineering and product owner: approved provider/runtime entitlement, unified customer API identity, working execution and atomic spending, actual product/terms | Not implemented. Cannot set COMMERCE_READY truthfully or sell API credits for a usable inference service yet. Close with real authorized upstream request, tenant isolation, budgets/debits, timeout/retry and refund-adjusted spend tests. |
| GitHub CI and CD | GitHub account owner: clear recorded runner billing restriction; engineering: verified deployment authentication/channel | Four observed runs, zero successes. New PR run `34240101119` failed before steps; scheduled run `34150966782` also failed before steps. Earlier runs explicitly cite billing lock; latest annotation unavailable. Current workflow has build/test/health only. Do not bypass restriction with account migration or claim native manual deployment is GitHub CD. Close with successful current-source checks and an authenticated deployment gate. |
| Real customer onboarding acceptance | Account owner: controlled test inbox/session through secure browser auth | No new signup email, confirmation click, authenticated profile persistence, second-session reload or password-change acceptance performed in this run. Existing behavior and source tests preserved. Close using an authorized real test identity without exposing passwords/tokens. |

No arbitrary live charge/refund, credential rotation, inference activation, or disabled business-email trigger was performed. The launch authorization is already recorded; the missing items are access, implementation, and evidence, not a request to repeat that approval.
