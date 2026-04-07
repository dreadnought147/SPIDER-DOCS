# Comic Stock — Clarifying Questions for Product Owners
## Phase 1 Checkout MVP — Consultation Agenda

> **How to use:** Bring these to your PO/mentor sessions. Each question flags a real ambiguity
> that will change how you build the system. Group them by topic. Record the answers directly
> in this doc — they become your decision log.

---

## PAYMENT

**Q1. Which payment gateway?**
South Africa has specific options — Yoco, PayFast, Paystack, Peach Payments. Each has different APIs, fee structures, and supported payment methods. Which one has the business already evaluated or has a preference for?
> _Why it matters:_ Gateway choice determines our integration pattern, test sandbox availability, and which payment methods we can offer. We need to start integration early.

**Q2. What payment methods are required for Phase 1?**
Card only? Card + EFT? Instant EFT (Ozow/Stitch)? SnapScan? Buy-now-pay-later?
> _Why it matters:_ Each method has a different UX flow. EFT is async (user pays, we wait for confirmation). Card is sync. This fundamentally changes the order state machine.

**Q3. How do we handle async payment confirmation (e.g., EFT)?**
If a customer pays via EFT, there's a delay before funds confirm. Do we hold the stock? For how long? What's the order status during this window?
> _Why it matters:_ Stock could sell out while waiting for EFT confirmation. We need a reservation/timeout policy.

---

## VOUCHERS

**Q4. Fixed denominations or custom amounts for gift vouchers?**
Can a customer buy a R150 voucher, or only R50/R100/R200/R500 tiers?
> _Why it matters:_ Custom amounts need more validation logic and a different UI. Fixed tiers are simpler and more predictable.

**Q5. Can a voucher partially pay for an order?**
If the order is R300 and the voucher is R200, does the customer pay R100 via gateway? Or must the voucher cover the full amount?
> _Why it matters:_ Split payment (voucher + gateway) requires a two-step payment flow. This is significantly more complex.

**Q6. One voucher per order, or stackable?**
Can a customer apply multiple voucher codes to one order?
> _Why it matters:_ Stacking changes the discount calculation logic and opens up potential abuse vectors.

**Q7. Do vouchers expire?**
If yes, what's the expiry period? South African Consumer Protection Act has implications here.
> _Why it matters:_ Expiry logic in the system + legal compliance. CPA Section 63(2)(c) — prepaid certificates can't expire within 3 years.

---

## DELIVERY

**Q8. Flat-rate or regional delivery fees?**
Is delivery R99 everywhere, or does it vary by province/distance from the warehouse?
> _Why it matters:_ Flat rate = simple. Regional = we need a fee lookup table or API integration with the logistics partner.

**Q9. Which logistics partner(s)?**
Courier Guy, Aramex, DSV, Pargo (locker pickup)?
> _Why it matters:_ Determines whether we need to integrate with their API for tracking, or just pass order details manually. Also affects delivery estimate calculations.

**Q10. Do you want to support pickup points / locker collection?**
Pargo and Paxi are popular in SA. This is a different delivery model than door-to-door.
> _Why it matters:_ Pickup changes the address capture flow entirely — user selects a point from a map instead of typing an address.

**Q11. Delivery to all 9 provinces, or limited regions initially?**
> _Why it matters:_ If limited, we need a service area check before the customer gets too deep into checkout.

---

## STOCK & INVENTORY

**Q12. Where does stock data live?**
Are we building the inventory system, or is there an existing warehouse management system we integrate with?
> _Why it matters:_ This determines if we own the stock database or consume it from an external API. Completely different architecture.

**Q13. What happens when a customer's cart item goes out of stock during their session?**
Real-time notification? Block at checkout? Remove from cart automatically?
> _Why it matters:_ Real-time stock sync is complex. We need to agree on the UX for this edge case.

---

## USER ACCOUNTS

**Q14. Is guest checkout ever on the roadmap?**
The case study says account-based. But is that a hard business requirement, or a Phase 1 simplification?
> _Why it matters:_ If guest checkout comes later, our order model needs to support orders without a user account from the start. Better to design for it now even if we don't build it.

**Q15. Social login (Google/Facebook) or email/password only?**
> _Why it matters:_ Social login reduces registration friction significantly, but adds OAuth integration complexity. Important for mobile-first.

---

## ORDER MANAGEMENT

**Q16. What order statuses does the business need to see?**
Pending > Paid > Processing > Shipped > Delivered > Returned? What's the minimum set?
> _Why it matters:_ The order state machine is a core architectural decision. Getting this right now prevents painful migrations later.

**Q17. Can a customer cancel an order after payment?**
If yes, at what point is cancellation no longer allowed? What's the refund flow?
> _Why it matters:_ Cancellation + refund touches payment gateway (refund API), stock (re-add), and email (notification). It's a full reverse flow.

**Q18. Who manages orders on the business side?**
Is there an admin dashboard needed in Phase 1, or do the founders use the gateway's dashboard + email?
> _Why it matters:_ An admin panel is a second application. If we can defer it to Phase 2, we should.

---

## TECHNICAL / INTEGRATION

**Q19. Any preferences on tech stack?**
Does the bootcamp mandate specific technologies, or is the team free to choose?
> _Why it matters:_ We want to choose based on team strengths and what enables fastest delivery.

**Q20. Is there a hosting budget or platform preference?**
Vercel, Railway, AWS, Azure student credits?
> _Why it matters:_ Affects CI/CD setup, deployment pipeline, and what services are available (managed DB, email, etc.).

---

## PROCESS NOTE FOR THE TEAM

After each PO session:
1. Record the answer next to each question.
2. If the answer creates new questions, add them.
3. Update requirements doc (Phase1_Requirements.md) with confirmed decisions.
4. Move confirmed items out of "clarify with PO" status on Miro.

**This document is your decision log.** Panelists want to see that you consulted, recorded, and acted on PO input — not that you guessed.
