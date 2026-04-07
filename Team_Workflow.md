# Comic Stock — Team Workflow & Role Allocation
## 4-Person Team Operating Model

---

## TEAM COMPOSITION & ROLES

| Member | Background | Primary Role | Owns |
|--------|-----------|-------------|------|
| **Benny** | CS | DevOps / Backend Engineer | Git workflow, CI/CD, testing infra, API development, code reviews |
| **CS Member 2** | CS | Frontend / Full-Stack Engineer | UI implementation, API integration, mobile-first responsive design |
| **InfoSys Member 1** | IS | Business Analyst / UX Lead | Requirements elicitation, PO consultation, user stories, Miro boards, BPM diagrams |
| **InfoSys Member 2** | IS | QA / Documentation Lead | Test case writing, acceptance testing, documentation, presentation prep |

> **Key principle:** Everyone touches everything. These are primary responsibilities, not silos.
> CS students review IS work. IS students review CS work. Cross-pollination is the point.

---

## GIT WORKFLOW — Trunk-Based with Short-Lived Feature Branches

```
main (protected — no direct pushes)
  │
  ├── feature/cart-management        (FR-01 to FR-04)
  ├── feature/payment-integration    (FR-05 to FR-08)
  ├── feature/delivery-flow          (FR-09 to FR-11)
  ├── feature/order-confirmation     (FR-12 to FR-14)
  ├── feature/voucher-system         (FR-15 to FR-17)
  ├── feature/auth                   (FR-18 to FR-19)
  └── fix/[short-description]        (bug fixes)
```

### Rules
- **Branch from `main`, PR back to `main`.**
- Branches live max 2 days. If it's taking longer, the scope is too big — split it.
- Every PR requires **at least 1 review** from someone outside your discipline (CS reviews IS, IS reviews CS).
- Squash merge to keep `main` history clean.
- Commit messages: `type(scope): description` — e.g., `feat(cart): add quantity validation`, `fix(payment): handle gateway timeout`.

---

## CI/CD PIPELINE (GitHub Actions)

```yaml
# Runs on every PR to main
on: pull_request → main

jobs:
  lint:        # Code formatting & style
  test:        # Unit + integration tests
  security:    # Dependency audit + SAST scan
  build:       # Verify it compiles/builds
  
# Runs on merge to main  
on: push → main

jobs:
  deploy:      # Auto-deploy to staging
```

### Pipeline Gates (PR cannot merge unless all pass)
1. Linting passes (ESLint / Prettier or equivalent)
2. All tests pass
3. Test coverage >= 80% on business logic
4. No high/critical security vulnerabilities
5. At least 1 approving review

---

## TESTING STRATEGY — Test First

| Layer | What | Who Writes | When |
|-------|------|-----------|------|
| **Unit Tests** | Cart calc, voucher validation, order total, stock check | CS members | Before/during feature code |
| **Integration Tests** | API endpoints, DB operations, gateway mock | Benny (backend) | Per feature branch |
| **E2E Tests** | Full checkout flow in browser | QA Lead + CS Member 2 | After feature integration |
| **Acceptance Tests** | Match requirements acceptance criteria | IS Members | Before PR approval |

### Test-first means:
1. Write the test that describes the expected behavior.
2. See it fail (red).
3. Write the minimum code to pass (green).
4. Refactor.
5. PR.

---

## SPRINT CADENCE

Given the 2-week bootcamp timeline:

| Day | Focus |
|-----|-------|
| 1-2 | Requirements finalization, PO consultation, architecture decisions, repo setup |
| 3-4 | Auth + Cart (FR-18, FR-19, FR-01 to FR-04) |
| 5-6 | Payment integration (FR-05 to FR-08) |
| 7-8 | Delivery + Order confirmation (FR-09 to FR-14) |
| 9-10 | Voucher system (FR-15 to FR-17) |
| 11-12 | Integration testing, bug fixes, polish |
| 13-14 | Presentation prep, final demo |

> **This is a guide, not a contract.** Adjust based on bootcamp schedule and what you learn from POs.

---

## DAILY STANDUP (15 min max)

Each person answers:
1. What did I finish?
2. What am I doing today?
3. What's blocking me?

Keep it on Miro — a simple kanban: **To Do | In Progress | Review | Done**

---

## HOW IS MEMBERS CONTRIBUTE TO CODE

IS members aren't expected to write production code from scratch, but they should:
- Write test cases (especially acceptance tests) — this is code.
- Write API request examples / Postman collections.
- Review PRs for requirements alignment ("does this actually do what the PO asked?").
- Pair with CS members on features — navigator role in pair programming.

---

## COMMUNICATION

- **Primary:** Whatever your team uses (WhatsApp/Discord/Slack) — one channel, no DMs for project decisions.
- **Async updates:** Commit messages + PR descriptions are documentation. Write them well.
- **Decision log:** PO_Clarifying_Questions.md — every PO answer goes here.
- **Miro:** Source of truth for visual artifacts (requirements board, BPM, kanban).

---

## WHAT PANELISTS ACTUALLY WANT TO SEE

Based on the case study notes, panelists evaluate:

1. **Cohesion** — Does the team work as a unit? Cross-review, shared understanding, no "I only did my part."
2. **Consultation** — Did you ask good questions? Did you record and act on the answers?
3. **Engagement** — Are all 4 members active? Can each member explain any part of the system?
4. **Delivery** — Does the checkout work? Can a customer pay? Not brilliant — **functional and reliable.**
5. **Process** — Is there evidence of a workflow? Git history, CI pipeline, test results, decision log.

> **The product doesn't need to be impressive. The team does.**
