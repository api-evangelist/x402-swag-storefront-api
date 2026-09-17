---
name: custom-print-studio
description: Turn a text prompt into a printable design, approve it, and order it on apparel.
api: x402 Swag storefront API
operations:
  - custom-menu
  - create-custom-design
  - get-custom-design
  - regenerate-custom-design
  - approve-custom-design
  - add-cart-item
  - create-checkout
---

# Custom Print Studio

1. **See the blanks** — `GET /api/custom/menu` (`custom-menu`) for printable products and options.
2. **Generate a preview** — `POST /api/custom/designs` (`create-custom-design`) with your prompt. Paid: `402` -> pay $0.50 USDC on Base -> retry.
3. **Inspect / iterate** — `GET /api/custom/designs/{id}` (`get-custom-design`); `POST /api/custom/designs/{id}/regenerate` (`regenerate-custom-design`, another $0.50) until happy.
4. **Approve** — `POST /api/custom/designs/{id}/approve` (`approve-custom-design`) to make it orderable.
5. **Order it** — add the approved design to the cart (`add-cart-item`) and run the buy-merch-with-usdc flow (`create-checkout` -> `pay-order`).

Note: regeneration is billed each call; approve before adding to cart. No dry-run for the order itself.
