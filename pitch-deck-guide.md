 # Pitch Deck Guide — Comic Stock Phase 1

**Total time: 30 minutes.**
**Order (from `context`):** Li → Li → Nat → Benny → Tshi.
**Narrative arc:** problem → us → market → solution → why it matters.

## Time budget at a glance

| # | Slide | Owner | Time |
|---|-------|-------|------|
| 1 | Welcome + Problem Statement | Li | 3 min |
| 2 | Who We Are | Li | 2 min |
| 3 | Comic Stock Market & Vision | Nat | 7 min |
| 4 | Wireframe Walkthrough | Benny | 6 min |
| 5 | Value Proposition | Tshi | 7 min |
| 6 | Closing + Q&A | All | 5 min |
| | **Total** | | **30 min** |

Slides 1 and 2 are short on purpose — get into the meat fast.
Slides 3, 4, and 5 are roughly equal so no one person dominates
the floor.

---

## Slide 1 — Welcome + Problem Statement
**Owner:** Li · **Time:** 3 min
https://miro.com/app/board/uXjVGo-XZxM=/?moveToWidget=3458764666785043794&cot=14
What to cover:
- Greet the panel, introduce the project name.
- Open with the gap: South Africa has no dedicated online comic
  book retailer. Comic readers either import from overseas
  (slow, expensive) or settle for whatever a general bookstore
  stocks.
- Frame it as a real audience — comic culture is a community,
  not a niche hobby.

Walk-away thought: *"There's a real gap and a real audience."*

---

## Slide 2 — Who We Are
**Owner:** Li · **Time:** 2 min

What to cover:
- Introduce the team: Benny, Li, Nat, Tshi.
- Mix of CS and InfoSys — the team covers analysis, design,
  testing, and code in-house.
- One sentence per person. Keep it human.

Walk-away thought: *"This team has the right mix to deliver this."*

---

## Slide 3 — Comic Stock: Market & Vision
**Owner:** Nat · **Time:** 7 min

What to cover:
- Comic Stock's vision: become South Africa's premier online
  comic book retailer within 5 years.
- The four pillars from the case study:
  1. Frictionless customer experience
  2. Curated inventory based on demand
  3. Fast fulfilment, reliable delivery, easy returns
  4. Community — comic culture is social
- Mobile-first strategy because that's where SA buyers are.
- Stock-based model (not drop-shipping) → quality control and
  faster fulfilment.
- Revenue model: direct sales of comic books + gift vouchers.
- Account-based system → builds a remarketing database.

Walk-away thought: *"This is a focused, specialised business
with a clear model — not a generic bookstore copy."*

---

## Slide 4 — Wireframe Walkthrough (the proof)
**Owner:** Benny · **Time:** 6 min

Three beats. Each beat has script pointers — short lines you
can say almost verbatim, or bend into your own voice.

### Beat 1 — Why checkout first (~1 min)

Script pointers:
- *"Before I walk you through the screens, I want to explain
  why we picked checkout as Phase 1 in the first place."*
- *"The reason is simple: without a working checkout, the
  business has no revenue. Everything else — recommendations,
  reviews, social features — is built on top of this."*
- *"It's also the riskiest part of the build, because it
  touches third parties: the payment gateway, the logistics
  partner, the email service. We wanted to validate those
  integrations early, not last."*
- *"So Phase 1 has a clear, bounded scope: get a customer
  from cart to confirmation, securely, end to end."*

Transition line:
- *"With that in mind, let me show you what we built."*

### Beat 2 — Walk through the digitized wireframe (~3 min)

Script pointers, screen by screen. Move at a steady pace —
roughly 30 seconds per screen.

**Home / Product Listing**
- *"This is the entry point. Comics are displayed with a
  cover image, title, price, and a short description — that
  description was added because of user feedback, which I'll
  come back to."*
- *"The whole card is tappable, mobile-first by design."*

**Product Detail**
- *"Tapping a comic opens its full detail — bigger cover,
  full description, price, and an Add-to-Cart button that's
  large enough to actually hit on a phone."*

**Cart**
- *"This is the screen we put the most thought into. The
  customer can see every item, change quantity using plus
  and minus buttons, remove an item, or clear the cart
  entirely."*
- *"The totals breakdown is right here — subtotal, VAT,
  shipping, and the grand total. We show all of it before
  the customer commits."*
- *"The voucher field sits inside the cart so customers can
  apply a code without leaving the screen."*

**Delivery Details**
- *"From the cart, the customer goes to delivery. If they're
  a returning user, their saved address is pre-filled — they
  just confirm it."*
- *"There's also a delivery notes field for things like
  'gate code' or 'leave at reception.'"*

**Payment**
- *"Payment is handed off to a secure third-party gateway —
  we don't store any card data on our side. The customer
  picks their preferred method: card, EFT, or mobile."*
- *"This is also where the order total is finalised so the
  customer sees exactly what they're being charged."*

**Confirmation**
- *"After payment succeeds, the customer lands on a short
  confirmation screen — just a thank you, the order number,
  and a delivery estimate. The full receipt goes to their
  email."*
- *"And that's the complete checkout flow: cart to
  confirmation."*

Transition line:
- *"Now I want to show you why some of these screens look
  the way they do."*

### Beat 3 — How user feedback shaped this (~2 min)

Script pointers:

Opening:
- *"Before we built the digitized version you just saw, we
  drew the whole flow on paper and tested it with five real
  people — two technical testers and three end users."*
- *"What we heard back changed the design in three specific
  ways I want to call out."*

Change 1 — Editable cart:
- *"In the paper version, the cart was read-only. Every
  single end user tried to change a quantity, and every
  single one of them got stuck."*
- *"One user said, 'I can't edit, and I can't delete from
  what I see.' That's the moment we knew the cart needed
  plus-minus buttons, a remove option, and a clear cart
  action — all of which you saw on the cart screen."*

Change 2 — Simpler confirmation page:
- *"In the paper version, our confirmation page repeated
  every detail the customer had already seen during
  checkout. One user told us, 'I've already seen them three
  times.'"*
- *"So we cut the on-screen confirmation down to the
  essentials — order number, thank you, delivery estimate
  — and pushed the full receipt to email."*

Change 3 — Comic descriptions:
- *"Users wanted to know what they were buying before they
  added it to the cart. One of them compared it directly to
  Netflix — 'a short blurb that tells you what the comic
  is.'"*
- *"So every comic on the listing now has a description.
  Small change, big effect on confidence at the point
  of decision."*

Closing line for the slide:
- *"The way we summed up the testing in our report was
  this: the bones are right, the flesh needed work. The
  flow itself works — what we needed to fix was the
  detail. And that's what the digitized wireframe is."*

Handoff to Tshi:
- *"And on that note, Tshi is going to take you through
  why all of this matters for the business."*

Walk-away thought: *"They didn't just design — they tested,
listened, and improved."*

---

## Slide 5 — Value Proposition
**Owner:** Tshi · **Time:** 7 min

What to cover:
- Why Comic Stock wins:
  - **Specialisation beats generalisation** — focused on
    comics, not competing with general bookstores.
  - **Account-based model** → remarketing + personalised
    recommendations.
  - **Gift voucher system** → captures the gift-buying market,
    a separate customer acquisition channel.
  - **Frictionless checkout** → fewer abandoned carts,
    more revenue.
- Tie each point back to a pillar Nat introduced in Slide 3.
  This is the cohesion moment — the deck folds back on itself.
- Close on the long-term vision: this checkout is the
  foundation, not the ceiling. Phase 2 builds the experience
  on top of it.

Walk-away thought: *"This is more than a checkout. It's a
deliberate first step toward a viable business."*

---

## Slide 6 — Closing + Q&A
**Owner:** All · **Time:** 5 min

- One sentence close: *"Phase 1 is the foundation. Phase 2
  builds the experience on top of it."*
- Thank the panel.
- Open the floor. Anyone can field a question — but the slide
  owner takes the lead on questions about their section, then
  hands off if needed.

---

## Cohesion rules — read before building slides

1. **Use the same language across slides.** If Slide 3 says
   "frictionless purchase journey," Slide 5 should not say
   "smooth buying experience." Pick one phrase and stay with it.
2. **Same visual style on every slide** — same fonts, same
   colours, same layout grid. Pick a comic-book-ish palette
   and commit.
3. **Max 3 bullet points per slide.** If you need more, it
   belongs on the next slide.
4. **Show, don't tell.** Slide 4 should be mostly wireframe
   screenshots, not text.
5. **One person speaks per slide — but everyone knows the
   whole deck.** If a panelist asks Tshi about the cart icon,
   Tshi should be able to answer or hand off cleanly.
6. **Rehearse the handoffs.** *"...and Nat will take you
   through the market."* Smooth transitions sell cohesion
   harder than any single slide.
7. **Time yourselves in rehearsal.** 30 minutes goes faster
   than you think. If you're 5 minutes over in rehearsal,
   you'll be 10 over on the day.

---

## What panelists actually score on

- **Cohesion** — does the team work as a unit?
- **Consultation** — did you ask the PO good questions and
  act on the answers?
- **Engagement** — are all 4 members active and able to
  explain any part?
- **Delivery** — does the work do what it claims to?
- **Process** — is there evidence of a workflow?

The product does not need to be impressive. The team does.
