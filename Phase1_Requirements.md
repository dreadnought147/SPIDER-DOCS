# Comic Stock — Phase 1: Checkout MVP
## Functional & Non-Functional Requirements

> **Format note for Miro:** Each requirement below is designed as a discrete card.
> On your Miro board, create two sections: **Functional Requirements** and **Non-Functional Requirements**.
> Each card should show: **ID | Title | Description | Acceptance Criteria**.
> Group functional requirements by domain (Cart, Payment, Delivery, Order, Voucher).
> Color-code by domain. Link dependencies with arrows.

---

## FUNCTIONAL REQUIREMENTS

### Domain: Cart Management

**FR-01 | View Cart**
- Customer can view all items currently in their cart with title, cover image, unit price, quantity, and line total.
- Acceptance: Cart page loads in under 2s, displays accurate totals, handles empty cart state gracefully.

**FR-02 | Modify Cart Quantities**
- Customer can increase/decrease quantity of any item or remove it entirely.
- Acceptance: Quantity changes reflect in line totals and cart total immediately. Quantity cannot exceed available stock. Minimum quantity is 1 (0 = remove).

**FR-03 | Cart Persistence**
- Cart contents persist across browser sessions for logged-in users.
- Acceptance: User logs out, logs back in — cart is intact. Cart merges if items were added while logged out (clarify with PO).

**FR-04 | Stock Validation at Cart**
- Cart reflects real-time stock availability. Out-of-stock items are flagged, not silently removed.
- Acceptance: If stock drops below cart quantity, user sees a clear warning and cannot proceed to checkout until resolved.

---

### Domain: Payment Processing

**FR-05 | Payment Gateway Integration**
- System integrates with a third-party payment gateway (e.g., Yoco, Paystack, or PayFast — clarify with PO).
- Acceptance: Customer is redirected to / presented with gateway UI. System receives success/failure callback. No card data stored on our side.

**FR-06 | Multiple Payment Methods**
- Gateway supports at least card payments and one additional method (EFT/mobile money — clarify with PO).
- Acceptance: Customer can select payment method before confirming. Each method completes the flow end-to-end.

**FR-07 | Payment Failure Handling**
- Failed payments show a clear error and allow retry without losing cart state.
- Acceptance: Cart and delivery info are preserved after failure. User is not charged. System logs the failure reason from gateway.

**FR-08 | Order Total Calculation**
- System calculates subtotal + delivery fee + voucher discount = final total. Displayed before payment.
- Acceptance: Breakdown is visible on checkout summary. Matches what gateway charges to the cent.

---

### Domain: Delivery Instructions

**FR-09 | Capture Delivery Address**
- Customer provides delivery address (street, suburb, city, province, postal code).
- Acceptance: All fields validated. South African address format. Stored with the order.

**FR-10 | Delivery Preferences**
- Customer can add delivery notes (e.g., "gate code 1234", "leave at reception").
- Acceptance: Free-text field, max 250 chars, saved with order, passed to logistics partner.

**FR-11 | Delivery Fee Calculation**
- System calculates delivery fee based on address/region (clarify fee model with PO — flat rate vs. regional).
- Acceptance: Fee displayed before payment confirmation. Updates if address changes.

---

### Domain: Order Confirmation

**FR-12 | Order Confirmation Screen**
- After successful payment, customer sees confirmation with: order number, items, delivery address, total paid, estimated delivery window.
- Acceptance: Confirmation displays within 3s of payment success. Order number is unique and sequential.

**FR-13 | Order Confirmation Email**
- System sends confirmation email with same details as the confirmation screen.
- Acceptance: Email sent within 2 minutes of order completion. Includes order number for reference.

**FR-14 | Order History**
- Customer can view past orders in their account.
- Acceptance: Lists orders with date, status, total. Customer can view order detail.

---

### Domain: Voucher System

**FR-15 | Purchase Gift Voucher**
- Customer can buy a gift voucher for a specified amount (clarify denominations with PO — fixed tiers or custom amounts).
- Acceptance: Voucher purchased through same checkout flow. Voucher code generated and delivered via email to recipient.

**FR-16 | Apply Voucher to Order**
- Customer can enter a voucher code at checkout to reduce the order total.
- Acceptance: Valid code applies discount. Expired/used/invalid codes show clear error. Partial use carries remaining balance (clarify with PO). Only one voucher per order (clarify with PO).

**FR-17 | Voucher Balance Check**
- Customer can check remaining balance on a voucher.
- Acceptance: Input code, see balance. No authentication required for balance check (clarify with PO — security implications).

---

### Domain: User Account (Minimum for Checkout)

**FR-18 | User Registration & Login**
- Customer must have an account to complete checkout (account-based model per case study).
- Acceptance: Register with email + password. Login persists via session/token. Password meets minimum complexity.

**FR-19 | Guest Browse, Account to Buy**
- Browsing does not require login. Checkout requires login.
- Acceptance: Unauthenticated users can add to cart but are prompted to login/register at checkout.

---

## NON-FUNCTIONAL REQUIREMENTS

### Security

**NFR-01 | No Card Data Storage**
- System never stores, logs, or transmits raw card/payment data. All payment handled by gateway.
- Measure: Zero PCI-DSS scope. Verified by code review and penetration testing.

**NFR-02 | HTTPS Everywhere**
- All traffic encrypted via TLS. No HTTP endpoints in production.
- Measure: SSL certificate active. HTTP requests redirect to HTTPS. HSTS header present.

**NFR-03 | Authentication Security**
- Passwords hashed with bcrypt/argon2. Sessions expire after inactivity. CSRF protection on all state-changing requests.
- Measure: No plaintext passwords in DB or logs. Session timeout configurable (default 30 min).

**NFR-04 | Input Validation & Sanitization**
- All user inputs validated server-side. SQL injection, XSS, and CSRF prevented.
- Measure: OWASP Top 10 addressed. Automated security scan passes in CI pipeline.

**NFR-05 | Voucher Code Security**
- Voucher codes are cryptographically random, not guessable or sequential.
- Measure: Codes are minimum 12 characters, alphanumeric. Brute-force rate-limited.

---

### Performance

**NFR-06 | Page Load Times**
- Checkout pages load within 2 seconds on 3G mobile connection.
- Measure: Lighthouse performance score > 80. Tested on throttled connection.

**NFR-07 | Payment Processing Time**
- End-to-end payment (click pay to confirmation) completes within 10 seconds excluding gateway time.
- Measure: Server-side processing < 2s. Total time tracked in monitoring.

---

### Reliability

**NFR-08 | Order Integrity**
- No duplicate orders from double-clicks or retries. Idempotent payment processing.
- Measure: Idempotency key on payment requests. DB constraint on order reference.

**NFR-09 | Graceful Degradation**
- If payment gateway is down, user sees a clear message — not a crash or blank screen.
- Measure: Gateway health check. Timeout handling. User-friendly error page.

---

### Usability

**NFR-10 | Mobile-First Responsive**
- Checkout flow works on mobile devices first, desktop second (per case study mobile-first strategy).
- Measure: Fully functional on 320px width. Touch targets minimum 44px.

**NFR-11 | Accessibility Baseline**
- Checkout meets WCAG 2.1 AA for core flows (form labels, color contrast, keyboard navigation).
- Measure: axe-core audit passes on checkout pages.

---

### Maintainability

**NFR-12 | Test Coverage**
- Minimum 80% unit test coverage on business logic (cart calculations, voucher validation, order creation).
- Measure: Coverage reported in CI. PRs blocked below threshold.

**NFR-13 | CI/CD Pipeline**
- All code goes through automated lint, test, security scan before merge.
- Measure: GitHub Actions pipeline runs on every PR. No direct pushes to main.

**NFR-14 | API-First Architecture**
- Backend exposes REST API. Frontend consumes API. Decoupled so mobile app can use same API later.
- Measure: API documented (OpenAPI/Swagger). No business logic in frontend.

---

## TRACEABILITY MATRIX (for Miro)

| Business Objective | Functional Reqs | Non-Functional Reqs |
|---|---|---|
| Frictionless purchase journey | FR-01 to FR-14 | NFR-06, NFR-07, NFR-10 |
| Customer trust & security | FR-05, FR-07 | NFR-01 to NFR-05 |
| Gift market capture | FR-15, FR-16, FR-17 | NFR-05 |
| Stock-based sales | FR-04 | NFR-08 |
| Revenue generation (get paid) | FR-05, FR-06, FR-08 | NFR-07, NFR-08, NFR-09 |
| Future scalability | FR-18, FR-19 | NFR-12, NFR-13, NFR-14 |

---

## HOW TO PRESENT ON MIRO

1. **Two main frames:** "Functional Requirements" (left) and "Non-Functional Requirements" (right).
2. **Sticky note cards** per requirement — color by domain (Cart=blue, Payment=green, Delivery=orange, Order=purple, Voucher=yellow, Security=red, Performance=grey).
3. **Draw dependency arrows** between related cards (e.g., FR-08 depends on FR-02 and FR-16).
4. **Traceability matrix** as a table frame below, linking business objectives to requirement IDs.
5. **Flag items marked "clarify with PO"** with a red dot — these become your consultation agenda.
