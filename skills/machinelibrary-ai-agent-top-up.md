---
name: Fund the prepaid balance as an agent (Stripe MPP)
description: Add prepaid USD credit to the authenticated Machine Library account from an agent with an MPP-capable payment client, using the challenge-then-retry flow the spec documents.
api: openapi/machinelibrary-ai-openapi.yml
operations: [createMppBalanceTopUp]
generated: '2026-09-19'
method: generated
---

# Fund the prepaid balance as an agent (Stripe MPP)

Only do this when the user has authorised a purchase. Machine Library's terms state that unused balance is **not refunded** except where law requires (Terms of Service 4.8), so this action is not reversible.

## Steps

1. **Request a challenge** — `createMppBalanceTopUp`: `POST /v2/payments/mpp/top-up` with `{"package": "usd-10"}`; allowed packages are `usd-5`, `usd-10`, `usd-25`, `usd-50`, `usd-100`, `usd-250`, `usd-500`, `usd-1000` (amounts in the spec's `x-payment-info.offers` are 500 to 100000 cents). The first authenticated request returns `402` carrying a Stripe MPP payment challenge.
2. **Settle** — retry the same request with the resulting Payment credential; `200` means the payment settled and the existing USD balance was credited.
3. **Handle the rest** — `400` malformed package or Payment credential; `401` missing/invalid account credential; `402` verification failure; `409` the payment is already being processed (do not re-fire — poll or wait); `503` agent payments are temporarily disabled.

Humans top up at https://machinelibrary.ai/payments; the A2A agent's `credit-top-up` skill and the hosted MCP tool `spacefrontiers_top_up_balance` sit on this same operation. ACP checkout sessions also exist at `POST /v2/acp/checkout_sessions` (405 on GET), but that path is not in the published OpenAPI.
