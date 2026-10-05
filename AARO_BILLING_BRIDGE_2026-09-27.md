# AARO shared accounts and credit bridge

- Owner: Farhan. Linear: GEN-10. Sites-managed source; GitHub production linkage remains unverified.
- API WILD keeps its public Site identity and existing Stripe merchant, products, webhooks, portals and customer mapping. AARO keeps its owner-only Site audience.
- AARO uses the existing confirmed Supabase account on yautmilnpllojugpmfgy. Its access token stays in a Secure, HttpOnly, SameSite=Strict host-only cookie for at most one hour. No refresh token/password is stored. API WILD signup/reset handles account creation and email verification.
- API WILD requires both a verified customer token and a server-only shared bridge key for reservations/settlement. Client prices, owner IDs and claimed charges are ignored.
- Additive migration 0008 records AARO reservations separately from API WILD money credits. Invoice-backed balances are scoped by account and live/test mode. Atomic reservations prevent concurrent overdrafts; one request key cannot dispatch twice.
- Confirmed model token usage settles once. Unknown provider or settlement outcomes remain held. Existing authenticated gateway maintenance also expires never-dispatched reservations and marks stale executions uncertain. It never automatically refunds unknown work.
- Draft tariff: input tokens + 4 times output tokens. Not a provider-cost or margin guarantee. It remains disabled unless AARO_USAGE_ENABLED=true and AARO_TARIFF_VERSION exactly matches aaro-token-units-2026-09-27.draft-1. Validate economic rates before enabling customer usage.
- AARO_BILLING_ENABLED is not enabled. Stripe connector currently requires reauthentication. CLI confirms existing account has live access only and explicitly rejects sandbox context. Real sandbox checkout, signed webhook, renewal, failed payment and refund acceptance are not completed. No real charges or email tests performed.
- Bangladesh eligibility remains server-verified; public currency toggle is not proof. Trial grant/abuse enforcement is separate pending work.
- Existing AARO prices retained: Bangladesh Free/456/789/1234 BDT and global 15/79/139 USD. API WILD keeps SmarT/NeRD/Newton/Alien wallet products. No duplicate products created.
- Validation: API WILD 266 tests; AARO 19 gateway tests plus 22 frontend tests; TypeScript and production builds. Deployment receipts are recorded separately in Linear once returned.
- Release checkout: commerce-billing-release. Unrelated dirty CRM work is preserved in commerce-backend-launch and excluded from this release.

## Close activation gates

1. Owner reconnects Stripe with sandbox access; do not paste secrets into chat.
2. Run actual sandbox lifecycle acceptance on isolated test configuration without replacing live merchant secrets or sending customer charges.
3. Confirm tariff economics, provider budget, Bangladesh eligibility and trial-abuse enforcement before customer rollout.
4. Enable accepted billing/usage configuration and verify one approved account from sign-in through inference and ledger deduction. Publish AARO to customers only with owner authorization.
