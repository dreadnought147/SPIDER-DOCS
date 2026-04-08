# Phase 1 — Checkout Process Flow

A swim lane view of the checkout process for Miro recreation.

## Actors (Lanes)

| Lane | Actor |
|------|-------|
| 1 | Customer |
| 2 | Comic Stock Frontend |
| 3 | Comic Stock Backend |
| 4 | Third-Party Services (payment, email, logistics) |

## Process Steps

1. Customer clicks **Checkout**
2. If not logged in → prompt login/register
3. Review cart (items, quantities, stock check)
4. Enter delivery address and notes
5. Apply voucher code (optional)
6. Review order summary (items + delivery + voucher = total)
7. Confirm and pay → backend creates order, sends to payment gateway
8. Payment success → confirm order, deduct stock, send confirmation email
9. Payment failure → preserve cart, allow retry
10. Customer sees order confirmation screen

## Decision Points

| # | Decision | Yes | No |
|---|----------|-----|-----|
| D1 | Logged in? | Continue | Show login |
| D2 | Stock available? | Continue | Show warning |
| D3 | Has voucher? | Validate and apply | Skip |
| D4 | Voucher valid? | Apply discount | Show error |
| D5 | Payment successful? | Confirm order | Preserve cart, retry |

## Edge Cases to Note

- Double-submit on Pay button
- Stock running out mid-checkout
- Payment timeout / no callback
- Session expiry during checkout
- Voucher covering full vs partial amount
