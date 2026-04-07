# Comic Stock — Phase 1: Checkout BPM Swim Lane Diagram
## Business Process Model — For Miro Recreation

> **How to build this on Miro:**
> 1. Create a swim lane diagram (Miro has a built-in template: search "Swimlane" in templates).
> 2. Create 4 horizontal lanes (actors below).
> 3. Use rounded rectangles for tasks, diamonds for decisions, circles for start/end events.
> 4. Connect with arrows showing flow direction.
> 5. Color decision diamonds red/amber — these are where things can fail.

---

## SWIM LANES (Actors)

| Lane | Actor | Description |
|------|-------|-------------|
| 1 | **Customer** | End user browsing and purchasing |
| 2 | **Comic Stock Frontend** | The web/mobile application UI |
| 3 | **Comic Stock Backend (API)** | Server-side business logic, database |
| 4 | **Third-Party Services** | Payment gateway, email service, logistics partner |

---

## PROCESS FLOW: Complete Checkout

### Start Event: Customer has items in cart and clicks "Checkout"

```
CUSTOMER                  FRONTEND                 BACKEND (API)            THIRD-PARTY
────────                  ────────                 ─────────────            ───────────

[Start: Click                                      
 "Checkout"]                                        
     │                                              
     ▼                                              
 ◇ Logged in? ──No──►  [Show Login/               
     │                   Register Modal]            
    Yes                      │                      
     │                  [Submit Credentials] ──►  [Validate Auth]          
     │                       │                    [Return Session Token]   
     │                  ◄────┘                       │                     
     ▼                                               │                    
 [Review Cart]          [Display Cart] ◄──────── [GET /cart]              
     │                   - Items, qty, prices     [Validate stock          
     │                   - Stock warnings          for each item]          
     │                   - Subtotal                  │                     
     ▼                                               │                    
 ◇ Stock issues? ─Yes─► [Show stock warnings]        │                    
     │                   [User adjusts cart] ──► [PUT /cart]              
    No                                            [Re-validate stock]     
     │                                               │                    
     ▼                                               │                    
 [Enter Delivery         [Delivery Address Form]     │                    
  Address & Notes]            │                      │                    
     │                   [Submit Address] ──────► [Validate address]      
     │                                            [Calculate delivery     
     │                                             fee]                   
     │                   ◄─── [Return fee] ──────    │                    
     ▼                                               │                    
 ◇ Has voucher? ─Yes──► [Enter Voucher Code] ──► [POST /voucher/validate]
     │                                            [Check: exists,         
    No                                             not expired,           
     │                                             has balance]           
     │                        ◇ Valid? ──No──►   [Return error message]  
     │                          │                [User re-enters or skips]
     │                         Yes                   │                    
     │                   ◄── [Apply discount] ──     │                    
     ▼                                               │                    
 [Review Order           [Order Summary Page]  ◄─ [GET /checkout/summary] 
  Summary]               - Items + quantities      [Calculate final:      
     │                   - Delivery address          subtotal              
     │                   - Delivery fee              + delivery fee        
     │                   - Voucher discount          - voucher discount    
     │                   - TOTAL TO PAY              = total]              
     ▼                                               │                    
 [Confirm & Pay]         [Submit Payment] ─────► [POST /orders]           
                                                  [Create order            
                                                   status=PENDING]        
                                                  [Generate idempotency   
                                                   key]                   
                                                      │                   
                                                  [Initiate payment] ──► [Payment Gateway]
                                                      │                   [Process payment]
                                                      │                      │
                                                      │                   ◇ Payment success?
                                                      │                   │           │
                                                      │                  Yes         No
                                                      │                   │           │
                                                  ◄── [Callback/webhook]  │    [Return failure]
                                                      │                   │           │
                                                   ◇ Success?            │           │
                                                   │        │             │           │
                                                  Yes      No             │           │
                                                   │        │             │           │
                                                   │   [Update order      │           │
                                                   │    status=FAILED]    │           │
                                                   │        │             │           │
                                                   │   [Return error] ──►│    ◄───────┘
                                                   │                      │
                                                   │   [Show "Payment     │
                                                   │    failed, retry"]   │
                                                   │   [Cart preserved]   │
                                                   │        │             │
                                                   │   [User retries ───►│ (loop back to
                                                   │    or abandons]      │  Confirm & Pay)
                                                   │                      │
                                                   ▼                      │
                                              [Update order               │
                                               status=CONFIRMED]          │
                                              [Deduct stock]              │
                                              [Deduct voucher balance]    │
                                                   │                      │
                                                   ├─────────────────────►│ [Send confirmation
                                                   │                      │  email to customer]
                                                   │                      │
                                                   ├─────────────────────►│ [Notify logistics
                                                   │                      │  partner (future)]
                                                   │                      │
 [See Confirmation  ◄── [Order Confirmation        │
  Screen]                Page]                ◄── [GET /orders/{id}]
  - Order number          - Order #                 
  - Items                 - Items                   
  - Total paid            - Total charged           
  - Est. delivery         - Delivery estimate       
  - Tracking (future)     - Delivery address        
                                                    
[End: Order Complete]                               
```

---

## KEY DECISION POINTS (flag these on Miro with red diamonds)

| # | Decision | Yes Path | No Path |
|---|----------|----------|---------|
| D1 | Is customer logged in? | Proceed to cart review | Show login/register |
| D2 | Stock issues in cart? | Show warnings, force resolution | Proceed to delivery |
| D3 | Has voucher code? | Validate and apply | Skip to summary |
| D4 | Voucher valid? | Apply discount | Show error, user retries or skips |
| D5 | Payment successful? | Confirm order, send emails | Show failure, preserve cart, allow retry |

---

## ERROR / EDGE CASES TO HIGHLIGHT ON DIAGRAM

Mark these with red annotation stickies on Miro:

1. **Double-submit prevention** — Disable "Pay" button after click. Backend uses idempotency key.
2. **Stock race condition** — Stock validated at cart AND at order creation. If stock depleted between, order fails gracefully.
3. **Payment timeout** — If no callback within X seconds, show "processing" state. Backend polls gateway or awaits webhook.
4. **Session expiry during checkout** — Save checkout state. Re-authenticate without losing progress.
5. **Voucher + payment split** — If voucher covers partial amount, gateway charges the remainder. If voucher covers full amount, skip gateway entirely (clarify with PO).

---

## MIRO LAYOUT GUIDE

```
┌─────────────────────────────────────────────────────────────┐
│  COMIC STOCK — PHASE 1 CHECKOUT PROCESS (BPMN)             │
├─────────────────────────────────────────────────────────────┤
│  ░░░ CUSTOMER ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  [actions the customer takes]                                │
├─────────────────────────────────────────────────────────────┤
│  ░░░ FRONTEND ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  [UI rendering, form validation, display logic]              │
├─────────────────────────────────────────────────────────────┤
│  ░░░ BACKEND API ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  [business logic, DB writes, validation, orchestration]      │
├─────────────────────────────────────────────────────────────┤
│  ░░░ THIRD-PARTY ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  [payment gateway, email service, logistics]                 │
└─────────────────────────────────────────────────────────────┘
```

Flow moves **left to right**. Each swim lane is a horizontal band.
Vertical arrows cross lanes when responsibility shifts between actors.
