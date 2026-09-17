---
name: buy-merch-with-usdc
description: Browse the x402 Swag catalog and buy a physical item end-to-end, paying per order in USDC on Base via x402.
api: x402 Swag storefront API
operations:
  - list-products
  - get-product
  - add-cart-item
  - get-checkout-rates
  - create-checkout
  - pay-order
  - get-order
---

# Buy merch with USDC (x402)

Free to browse and build a cart; the order pays per-order in USDC on Base (eip155:8453) via x402. No API key.

1. **Find a product** — `GET /api/products` (`list-products`; filter with `q`, page with `limit`/`offset`) then `GET /api/products/{handle}` (`get-product`) for variants and prices.
2. **Add to cart** — `POST /api/cart/add` (`add-cart-item`) with the variant id and quantity. The cart is stateless: keep the returned cart id and pass it back via the `X-Cart-Id` header, a `cart_id` body field, or `?cart_id=`.
3. **Check rates** — `GET /api/checkout/rates` (`get-checkout-rates`) for shipping/total on the cart.
4. **Create the order** — `POST /api/checkout` (`create-checkout`) with `email` and `shipping_address` (country required). Handle `422` (validation) and `503` (fulfilment/payment upstream down).
5. **Pay** — `POST /api/orders/{token}/pay` (`pay-order`). You get `402 Payment Required` with x402 terms in the `PAYMENT-REQUIRED` header/JSON body; pay USDC on Base and retry with the payment header. Card alternative: `POST /api/orders/{token}/stripe`.
6. **Confirm** — `GET /api/orders/{token}` (`get-order`).

Conventions: no Idempotency-Key is documented, so do not blind-retry a write; poll `get-order` to confirm. Payments settle on-chain and are NOT reversible — there is no cancel/refund operation in this API.
