---
name: agent-catalog-one-call
description: Get the full product catalog plus the buy flow in a single paid x402 call, for agent planning.
api: x402 Swag storefront API
operations:
  - get-agent-catalog
---

# One-call agent catalog

`GET /api/agent/catalog` (`get-agent-catalog`) returns the entire product catalog with prices, variant ids and the buy flow in one response — purpose-built for an agent to plan a purchase without walking every product route.

- Paid: answers `402 Payment Required`; pay $0.05 USDC on Base (eip155:8453) and retry with the payment header. Handle `503` (upstream) with backoff.
- This route is Bazaar-discoverable via `/.well-known/x402.json`.
- Follow up with the buy-merch-with-usdc flow using the ids it returns.
