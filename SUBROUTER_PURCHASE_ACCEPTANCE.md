# API WILD — SubRouter purchase and acceptance sheet

Status: **OWNER APPROVAL REQUIRED — NOT PURCHASED — NOT ACTIVATED**  
Prepared: 2026-09-26  
Scope: API WILD only. The approved UI, Site identity, no-playground scope, and deferred logo change are preserved.

## 1. Read-only inventory

| Item | Independently observed | Acceptance requirement |
|---|---|---|
| Distributor station | ¥388 first year, limited-time offer, instant activation | Farhan approves the exact charge in the browser |
| Renewal | Not disclosed on the order page | Written renewal price or an owner-accepted ceiling before purchase |
| Payment methods | Alipay, WeChat Pay, USDT, USDC | Farhan chooses the payment rail; no wallet deposit by the agent |
| Marketplace | 91 providers; 1,762 marketplace listings; 1,297 priced model entries; 18 vendor groups | Re-count after station activation and record a dated export |
| Current SubRouter account | ¥0 balance; ¥0 spend; 0 requests; 91 followed providers | Followed is not treated as subscribed until distributor API proves it |
| White-label controls | Custom domain, name, logo/favicon, announcements, registration mode, currency display, model visibility, top-up, global/per-model markup | Configure only API WILD branding; logo remains unchanged until separately approved |
| API families | OpenAI-compatible chat/responses/models plus Anthropic messages; documented audio, embedding, rerank, moderation, realtime, image/video surfaces | Only text chat is enabled at launch; every other surface stays unavailable until independently tested |
| Customer currency | Custom display exists; package settlement is documented in CNY | BDT checkout/settlement is **not verified** and must not be advertised |
| Customer payments | Station payment credentials are owner-entered in the console | API WILD Stripe remains the only planned customer payment authority |
| Existing paid provider balances | YouPai ¥1; dddAI ¥0.10; Z-API $0; no active subscriptions/orders observed | Do not combine or transfer balances without owner approval |

## 2. Architecture decision

- Customer identity and onboarding authority: Supabase project `yautmilnpllojugpmfgy`.
- Customer payment authority: API WILD Stripe account and exactly-once API WILD ledger.
- Customer usage authority: API WILD D1 reservation/debit ledger.
- Upstream procurement authority: SubRouter owner wallet and provider receipts.
- Customer-facing UI: the existing API WILD Site only; no SubRouter playground.
- API keys: API WILD keys are customer-facing. A SubRouter credential is server-side only and must never reach the browser, source, logs, or Linear.
- Cost records: the existing `together_*` D1 fields remain as a legacy-compatible text-upstream bucket for this acceptance release. The API and evidence label the actual provider as `subrouter`; a schema rename is deferred until historical reconciliation is complete.

## 3. Proposed domain and branding

- Station domain: `router.apiwild.com` (proposed; DNS/SSL steps must be verified after purchase).
- Public product domain: `apiwild.com` remains unchanged.
- Station name: `API WILD`.
- Logo/favicon: preserve current assets; replacement remains deferred.
- Provider identity: hide upstream provider information from customers only after legal/resale terms are accepted; retain provider identity in internal receipts.

## 4. Initial model allowlist

The marketplace contains many routes, but production exposure is fail-closed. Only models that pass the five-call test and a price ceiling may enter the API WILD allowlist.

| API WILD route | Candidate upstream model | Observed cheapest advertised CNY / 1M input | Observed cheapest advertised CNY / 1M output | Production status |
|---|---|---:|---:|---|
| `apiwild/chat` | `gpt-6-astra` | ¥0.145147 | ¥0.725735 | Blocked pending real call and receipt |
| `apiwild/code` | `deepseek-v4-flash` | ¥0.013235 | ¥0.052941 | Blocked pending real call and receipt |
| `apiwild/research` | `deepseek-v4-pro` | ¥0.029412 | ¥0.058824 | Blocked pending real call and receipt |
| future | `claude-fable-5` | ¥0.179412 | ¥0.897059 | Discovery only |
| future | `gemini-3.5-flash` | ¥0.176471 | ¥1.058824 | Discovery only |
| future | `qwen3.7-plus` | ¥0.213235 | ¥0.852941 | Discovery only |

- These are advertised marketplace values, not accepted landed costs.
- Cheapest routes can be anomalous. A route is rejected if identity, usage, receipt, latency, output, availability, or billed cost cannot be independently reconciled.
- Proposed retail rates are not activated: Chat $0.50/$2.50, Code $0.20/$0.80, Research $0.30/$1.00 per 1M input/output tokens, plus verified search cost. Final rates require the actual CNY-to-USD landed rate, fees, tax, failure allowance, and margin calculation.

## 5. Markup and wallet controls

- Proposed station global markup: 100% only as a starting ceiling; per-model overrides must never price below landed cost plus payment, FX, tax, retry, and support allowance.
- API WILD customer credits and SubRouter upstream funds must never be treated as the same wallet.
- Only Farhan may authorize station purchase, deposits, payment credentials, production API credentials, or a spending-cap increase.
- Daily upstream cap before launch acceptance: ¥5 equivalent total.
- Per-call acceptance cap: ¥1 equivalent.
- No automatic provider fallback during acceptance; each call must identify one chosen route.

## 6. Five bounded acceptance calls

1. `GET /v1/models`: no paid usage; verify authenticated response, selected model IDs, and no secret exposure.
2. OpenAI chat call to the Chat candidate: maximum 64 output tokens; verify response ID, exact model, token usage, finish reason, provider receipt, latency, and wallet debit.
3. Anthropic messages call to the Claude candidate: maximum 64 output tokens; verify compatibility, usage, receipt, and debit.
4. OpenAI Responses/tool-format call: maximum 64 output tokens and one harmless schema-only tool; verify structured output without executing external actions.
5. DeepSeek code call: maximum 64 output tokens; verify exact model identity, usage, receipt, and debit.

## 7. Stop conditions

- Stop immediately if the renewal price is undisclosed and Farhan has not accepted a renewal ceiling.
- Stop before any charge greater than ¥388 for the station or ¥5 total acceptance spend.
- Stop if a credential would be exposed to the browser, repository, command output, or Linear.
- Stop if the model returned differs from the allowlisted model or the route silently substitutes another model.
- Stop if usage fields, provider receipt, or wallet debit cannot be reconciled.
- Stop if a single call exceeds ¥1 equivalent, the cumulative test spend exceeds ¥5, or a retry could double-charge.
- Stop if the provider terms do not permit commercial resale/white-label use.
- Stop if BDT display is mistaken for BDT settlement.
- Stop if Supabase owner-controlled signup/confirmation/onboarding/signout/fresh-session recovery is not proven.
- Stop if Stripe payment, exactly-once credit, refund/dispute handling, or provider-response/debit reconciliation is not proven.
- Keep `BILLING_ENABLED=false`, `COMMERCE_READY=false`, `GATEWAY_ENABLED=false`, and `GATEWAY_ACCEPTANCE_VERIFIED=false` until every applicable gate passes.

## 8. Exact approval requested

- Approve one SubRouter distributor station purchase at **¥388 maximum**.
- Approve a separate **¥5 maximum** upstream acceptance-test spend.
- Accept that the renewal price is currently unknown and require a written renewal price or owner-approved ceiling before renewal.
- Approve proposed station domain `router.apiwild.com`.
- Do not approve customer billing or public inference activation yet.
