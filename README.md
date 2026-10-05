# API WILD

API WILD is a Sites/vinext application for model discovery, customer accounts and planning. The original supplied Deal Desk reference remains below and its HTML/assets remain at the repository root; it is not the current runtime.

## Current runtime

- React/vinext app routes in `app/`, Cloudflare Worker and D1 billing/legacy data.
- Supabase Auth and RLS-protected customer onboarding. Support runs as a separate Supabase Edge Function.
- Catalog browsing and profile management are implemented. Stripe reconciliation code is guarded; inference, credit consumption and six advanced console sections are not implemented for customer use.
- See `PRODUCTION_REVIEW_2026-09-08.md` for the acceptance matrix and `DEPLOYMENT_EVIDENCE.md` for the actual deployed version. A successful source build does not establish paid-service readiness.

## Development and verification

Use the Sites-managed checkout. `npm run install:ci` installs locked dependencies, `npm test` performs the production build and source tests, and `node_modules/.bin/tsc --noEmit --incremental false` checks types. Use `sites-preview start /workspace/sites/api-wild` for the supported local browser preview and `sites-preview stop` when finished. Never commit `.env*` or `.dev.vars*`.

GitHub hosts a reviewed public source export and scheduled checks. Production publishing uses saved Sites versions; the GitHub workflow does not itself deploy the Site.

---

## Original supplied reference README

# Deal Desk — by RenoWave Builders

A futuristic Web3 payments site for a real estate & construction company. Accept card (Stripe on-ramp) or crypto payments for property development, construction milestones, renovation/painting, NFT deeds and Web3 escrow.

**Domain:** dealsdesk.io

## What's inside
- `Deal Desk.dc.html` — the full multi-page site (Home, Services, Pay, About) as a single streaming Design Component.
- `support.js` — runtime for the Design Component (required; load alongside the HTML).
- `assets/projects/` — generated project render images used by the card-fan carousel.

## Features
- Interactive **Spline 3D** hero with spotlight + mouse parallax.
- **Liquid-glass** primary buttons (SVG turbulence/displacement + glass-rim).
- **GlowHorizon** section with an animated card-fan carousel of renovation projects.
- Multi-step **payment flow**: select service → amount → method (card / crypto) → review → confirmation.
- Live **theme switcher** (cyan / violet / green) and a consistent line-icon system.

## Run locally
It's a static site — serve the folder with any static server, e.g.:

```bash
npx serve .
# then open "Deal Desk.dc.html"
```

> Note: This is a high-fidelity **frontend demo**. Live Stripe on-ramp and on-chain escrow settlement require backend keys and smart-contract integration, which are not wired up here.

## License
© 2026 RenoWave Builders. All rights reserved.
