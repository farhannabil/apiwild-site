## Gateway release v21 — 2026-09-08 15:59 UTC

1. Site/service: API WILD, project appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d; public custom domain https://apiwild.com; native deployed URL https://legacy-ai-exchange.genxintel-6787.chatgpt.site. Supabase production yautmilnpllojugpmfgy, support-inbound v5 ACTIVE freshly verified.
2. GitHub repository: farhannabil/api-wild. Existing draftPR1 https://github.com/farhannabil/api-wild/pull/1 now head ae425db35d313a8ea5dc3ec68b475887b43bfed6, tree318d8f9b7275e7f2ccd90b34dea7da0df0e0aa75. Exactly43 changed public files exported; native commit read confirms43 files. Main remains06d05055c7d5cb228287c857fecba6867eb4442e, unmerged. New run34247899042 build-and-test job102134512433 failed with an explicitly empty step list; production-health job102134513818 skipped. Five observed failed runs and zero successes. Account restriction remains owner-controlled; no repeated rerun or workaround.
3. Production commit: da25a872fb274b525848b27ebd0eaf25d6121632, saved/deployed v21, version appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d~appgver_3496a8d82e0481919db00d9f5c095a68. Sites-managed Git remains distinct from GitHub. This is the user-authorized native release, not a successful GitHub-triggered deployment.
4. Linear: GEN-10 / 6cd15598-15af-44a3-864c-7e471045b6de. Start comment0f7d66e9-8f84-46d9-99bd-57c076d62d56; implementation comment00964dba-c397-4075-9542-6423b29700cd; final exact release checkpoint follows.
5. Owner: Gen X Intel / Farhan Nabil; Site owner contact@genxintel.com. Native current Site role remains editor. Previously denied owner-only runtime access is not retried. Live connection is already authorized; secure configuration and actual evidence are the outstanding requirements, not another request for the same approval.
6. Deployment evidence: appgdep_6aa0306fff848191957f6a4eb699a253 succeeded2026-09-08T15:58:34.586731+00:00, environment revision6. Native saved archive content hash sha256:1d925cf92a05a2aaf8b6a5bc91c7fc7e2deed5ad2a1a5b9e8e2a01dd04ad866e. Local compressed archive sha2560f60f8d47eee429208a7bbef787f6c029d8846e59694ce65e5446ae7e56a1862,271 entries; contains Worker and all six generated D1 migrations; no development environment or private handoff files.

Post-release HTTP at15:59UTC: /pricing200 with new service/credit copy; /api/gateway/config200, routes apiwild/chat, apiwild/code, apiwild/research, tariff2026-09-08.1; enabled=false and all six readiness flagsfalse. /api/gateway, /api/gateway/keys, /v1/models and /api/billing each401 without authentication. These are verified deployed outcomes; no inference availability is inferred. Browser preview verified route/credit cards, model search, anonymous console→login and password visibility controls. Auth/onboarding/email/support sources have zero diff against deployedv20; v19 behavior is preserved.

Verification:94/94 actual-migration tests PASS with intercepted provider/Stripe/Supabase responses, TypeScriptPASS, production Worker buildPASS. Covers duplicate dispatch/replay, cross-key isolation, budget concurrency, unknown holds, receipts, audio recovery, partial/full refunds after spending, terminal failures, no-return reconciliation, support/email canonical sender invariants, receipt-free operator interruptions, stale resolution races and exact export acknowledgements. No live provider credits, real payments/refunds, customer signup or emails were used by these tests.

Open owned gates: secure Stripe/provider keys and positive provider budgets; commercial/promo rights and a sustainable tariff decision; actual external financial/provider acceptance; GitHub billing/runner restriction; matching secure gateway-maintenance secret in GitHub/Sites and a successful recurring run; actual external outbox delivery if selected. Code is a write/review assistant, not repository execution; voice is recorded turns, not full-duplex telephony; arbitrary model/image execution and business connectors are not implemented. Other business emails remain disabled, Stripe remains canonical for financial messages, support acknowledgement remains deduplicated. See plans/GATEWAY_IMPLEMENTATION_2026-09-08.md for exact configuration/action/closing-evidence mapping.

Existing daily operations and merge-only release automations were updated and read back enabled with implementation authorization; schedules preserved, no duplicate tasks. Successful exact-main checks/review/merge remain mandatory for automatic release. No continuation prompt.

## Implemented gateway operations — September 8, 2026

The user authorized implementing Chat, Code, Research and recorded voice. Read plans/GATEWAY_IMPLEMENTATION_2026-09-08.md. Prior planning-only/no-playground restrictions no longer apply to this implementation. Existing USD 25/100/250 prepaid packs remain unchanged; monthly subscriptions, external metering contracts and new provider contracts require a commercial decision.

Current gateway regression suite has 94 passing mocked-provider tests. Live provider/payment acceptance is still unverified. Scheduled health now checks route availability, protected customer APIs and maintenance. Configure APIWILD_GATEWAY_OPERATIONS_SECRET in GitHub Actions to match Site GATEWAY_OPERATIONS_SECRET through owner-controlled secure settings; missing configuration reports a failed maintenance gate. POST /api/gateway/maintenance is idempotent and bounded. GET /api/gateway/operations lists uncertain requests and pending usage exports. Operator resolution requires provider receipts/cost evidence, returns zero customer charge for unrecoverable output and enforces a stale-write check. Export acknowledgements count actual transitions and retain their canonical delivery receipt. Do not invent automatic provider reconciliation or external meter delivery.

Preserve verified v19 auth behavior and deployed v20 support v5 source. All 43 changed public-source files for this implementation were exported to existing draft PR1 at ae425db35d313a8ea5dc3ec68b475887b43bfed6, tree318d8f9b7275e7f2ccd90b34dea7da0df0e0aa75. GitHub main is unchanged and actual runner acceptance remains open. Do not merge failed CI or use a different account/runner to bypass the provider restriction. The root's user-authorized native Sites release is distinct from a successful GitHub-triggered release.

## Product proposal and delivery configuration — 2026-09-08, approximately 15:04 UTC

1. Site/service: https://apiwild.com, existing Sites project appgprj_6a9d1c56b1f08191a5ccf98fddb6f83d; Supabase yautmilnpllojugpmfgy. No application runtime change in this planning turn.
2. GitHub: farhannabil/api-wild, draft PR1 head 4e0931c4a2daa2421a21f2634ee756bff204a89a, main 06d05055c7d5cb228287c857fecba6867eb4442e. Exact public PR tree independently reconstructed and passed 64 tests, TypeScript and build using installed locked dependencies. Fresh install not retested. Four observed GitHub runs remain failed, zero successes; latest 34240101119 failed before steps. Earlier account billing restriction remains unresolved; no unjustified YAML patch, rerun, merge or migration.
3. Production: v20/source 841254ad40ceb1eb5545f7ca0b374bce7cd7c4e4 remains live, preserving v19 auth. New planning/source checkpoints are not deployed versions.
4. Linear: GEN-10, read and start comment 78fda3bb-9a5c-43d4-841a-a9470ea5c1f5 written before changes; exact final configuration/results recorded after source push.
5. Owner: Gen X Intel / Farhan Nabil. GitHub owner must resolve the actual farhannabil account restriction at https://github.com/settings/billing. GENXSTARK is the intended namespace, access/migration unverified. Stripe live connection already authorized; local CAPTCHA and secure owner runtime settings are unresolved access/evidence dependencies, not a request to approve live again.
6. Evidence: existing succeeded deployment appgdep_6aa01eaa8a3c8191ad6d03fd280b752a at 14:42:01.787792 UTC, environment revision6/public; support-inbound v5 re-read ACTIVE. Native API WILD merged releases task 6aa023e6cca0819199d83101caf8a0d9 created successfully and re-read enabled, no runs yet. Trigger: GitHub pull_request on farhannabil/api-wild, only_on_merge=true, no independent schedule. Exact successful main checks, reviewed source, duplicate/concurrency controls and native Sites release verification are mandatory. Existing daily task 6a9ea5c2b7dc8191af3bb72293786d0c updated successfully to re-evaluate recorded deferred merged releases; existing schedule preserved. This is configured agent-mediated delivery, not proven uninterrupted CI/CD.

Research deliverables: plans/PRODUCT_AND_BILLING_PROPOSAL_2026-09-08.md, plans/PROVIDER_RESEARCH_2026-09-08.md, plans/STRIPE_METERED_BILLING_2026-09-08.md and plans/CI_DELIVERY_2026-09-08.md. Proposed Everyday/Builder/Workflows tiers, shared private provider accounts, bounded prepaid usage, illustrative USD19/49/149 pricing with retail allowances10/30/100. These are not approved products. Stripe's Metronome is the recommended advanced usage-rating target, subject to actual plan economics; local atomic reservation is the immediate spending control.

Critical design finding: current credit_ledger has no entry kinds and refund/dispute queries treat all negative order entries as refunds. Do not append usage spending to it unchanged. Typed accounting or a separate usage/reservation ledger, micro-units, purchase-lot allocation, permanent idempotency and one authoritative transactional balance are prerequisites.

The latest request is to plan provider spending with the user. No new Stripe products, customer prices, keys, contracts, charges/refunds, inference/API gates or disabled emails changed. Auth and deduplicated support remain preserved. Local-browser instruction: this session only exposes cloud CDP and cannot launch the user's browser; provide https://dashboard.stripe.com/login for local completion, with no claim that cookies transfer. No continuation prompt is requested.

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

# API WILD operations

The website and support receiver are separate deployments. Passing CI does not prove that a GitHub commit has been deployed.

## Support email

Supabase Edge Function `support-inbound` consumes only signature-verified Resend `email.received` events addressed to `support@apiwild.com`. Messages are retained in Resend Receiving. Acknowledgements use `API WILD Support <support@apiwild.com>` with Reply-To at that same address. They do not promise a response time, resolve tickets, or answer customer questions automatically.

Server-only Supabase secrets: `RESEND_API_KEY`, `RESEND_WEBHOOK_SECRET`, `SUPPORT_AUTOREPLY_ENABLED=true`. Never put these in GitHub source, public CI artifacts, or the browser application. The receiver uses platform-provided database service credentials.

The delivery ledger and atomic leases prevent repeated sends from duplicate events and concurrent workers. Ambiguous retries reuse the frozen payload and Resend idempotency key for at most23hours, below Resend's24hour retention; older attempts require operator review. Replies from automated senders, own-domain mail, mailing lists and follow-up threads are suppressed. Limits are one acknowledgement per sender per24hours and75total per24hours; additional messages still arrive in Resend. These are conservative initial limits, not a support-response SLA. Delivered payloads are cleared after30days while dedup identifiers remain.

Daily database job `apiwild-support-daily-health` runs at13:17UTC, records aggregate delivery health, marks expired attempts for review and clears old delivered payloads. It does not delete incoming support mail. Inspect `support_daily_health` and `support_deliveries` using an authorized service/admin account. These tables deliberately grant no customer access. A `review` row requires human reconciliation with Resend before any new send; never reset it blindly.

Disable automatic replies by setting `SUPPORT_AUTOREPLY_ENABLED=false` in Supabase. Keep the webhook configured; failed events can retry. Restore only after verifying the receiver and credentials. Do not re-send an already-acknowledged message.

## CI and daily external checks

`.github/workflows/apiwild.yml` builds and runs tests for main commits, pull requests, manual runs and a daily schedule around08:17America/Winnipeg. It checks public routes, model data, auth boundaries, email DNS and the support endpoint. No customer signups, password resets or payment charges occur during daily checks.

The workflow uses pinned GitHub actions and read-only repository access. It never receives Resend credentials. `scripts/prepare-ci.mjs` creates a generic build-only hosting configuration when an exported repository omits the private Sites identity. Never deploy that temporary configuration.

GitHub scheduled workflows can be delayed and public repository schedules can disable after60days of repository inactivity. The separate daily operational review checks for missing/failed runs. An empty or unreachable repository is a failure, not a healthy pipeline.

Production publication stays with the verified Sites deployment process. A GitHub Actions runner must not fabricate Sites credentials or deploy unverified billing. Support Edge Function updates need the matching Supabase deployment authorization; this CI workflow only validates code. Commerce receipt/welcome/API-key delivery remains gated by its actual authenticated business event and verified payment configuration.

## Release checks

Routine reversible maintenance is authorized: investigate a concrete failure, prepare a focused branch/PR, inspect the diff, run the existing build/tests, then use the established verified release process when its gates pass. Preserve the current Site identity and audience. Record the deployed commit and post-release health; a saved version or successful source push is insufficient. Do not redeploy the website for monitoring-only changes. Do not enable commerce or transactional email until the corresponding authenticated event and provider acceptance are verified.

The daily operational review must inspect the latest scheduled run and latest successful run separately, alert when no scheduled run has arrived for more than36hours, and investigate any failing or missing jobs. A schedule that fired but failed before execution is not healthy CI. If GitHub blocks runners at account level, report the specific provider restriction and avoid repeated reruns until it is cleared. Keep independent website, database and support checks running. Resolve available independent release gates while an owner-only gate remains blocked.

For repository consolidation, verify the designated destination account, repository visibility and access before changing remotes. Preserve history, the original repository and private export exclusions. API WILD readiness takes priority over unrelated migrations; account migration never substitutes for resolving a provider restriction.

1. Run the existing build and tests (`npm test`).
2. Review provider/configuration changes separately from application diffs.
3. Apply new database migrations once and verify service-only grants.
4. Deploy the receiver and check `/health` plus unsigned-request rejection.
5. Verify an owner-controlled support message produces one delivered acknowledgement. Replay its signed event and verify no second send.
6. Record actual source commit, provider function version, migration and delivery evidence privately; publish no secrets or customer mail in repository issues.

Reference documentation: [Resend signatures](https://resend.com/docs/webhooks/verify-webhooks-requests), [Resend idempotency](https://resend.com/docs/dashboard/emails/idempotency-keys), [Supabase Cron](https://supabase.com/docs/guides/cron), [GitHub schedules](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule).
