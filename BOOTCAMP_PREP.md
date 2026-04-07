# Bootcamp Prep — What to Have Ready Before Day 1
## Comic Stock Phase 1: Checkout MVP

> You don't know exactly what they'll throw at you. This checklist makes you
> dangerous regardless of direction. Don't build anything yet — just be ready to.

---

## BEFORE YOU SLEEP TONIGHT

### 1. Accounts & Tools — Have These Logged In and Working

- [ ] **GitHub** — account ready, SSH key configured, can push/pull without password prompts
- [ ] **Miro** — account ready, team board created (even if empty), invite link ready for teammates
- [ ] **IDE** — IntelliJ IDEA (Community is free) OR VS Code with Java Extension Pack installed. Either works. Have both if you're unsure what the team will use
- [ ] **Node.js + npm** — installed (needed for Angular regardless of backend). Run `node -v` and `npm -v` to confirm
- [ ] **Java 17+ JDK** — installed. Run `java -version` to confirm. Use Eclipse Temurin or Amazon Corretto (both free)
- [ ] **Angular CLI** — `npm install -g @angular/cli` then `ng version` to confirm
- [ ] **Postman or Insomnia** — installed for API testing (free tier)
- [ ] **Git** — configured with your name and email (`git config --global user.name` / `user.email`)
- [ ] **Docker Desktop** (optional but useful) — if they give you a containerized DB or want you to deploy with containers, you're ready

### 2. Know Your Case Study Cold

You should be able to explain these without looking at the doc:

- [ ] **What is Comic Stock?** — SA's premier online comic book retailer (startup, 2 founders)
- [ ] **What is Phase 1?** — Checkout MVP. Cart → Pay → Deliver → Confirm. Plus vouchers.
- [ ] **What's outsourced?** — Accounting, legal, payment processing (3rd party gateway)
- [ ] **What are the 4 business pillars?** — Superior UX, comprehensive selection, exceptional service, community
- [ ] **What's the revenue model?** — Direct comic sales + gift vouchers
- [ ] **What's the inventory model?** — Stock-based (not drop-shipping), stocked based on market analysis + sales patterns
- [ ] **What are the success criteria?** — Production-ready checkout, payment flow validated, third-party integration patterns established, architecture that supports future phases
- [ ] **What do panelists care about?** — Cohesion, consultation, engagement, delivery (that you get paid), team process

### 3. Have Your Clarifying Questions Ready

- [ ] Read through `PO_Clarifying_Questions.md` — know which questions are yours to ask
- [ ] Star the top 5 most critical (payment gateway choice, voucher rules, delivery fee model, order statuses, tech stack confirmation)
- [ ] Be ready to ask them in the first PO session — don't wait

### 4. Understand the Docs You Have

| File | What It Is | When You'll Use It |
|------|-----------|-------------------|
| `Phase1_Requirements.md` | Functional + non-functional requirements | Transfer to Miro as your requirements board |
| `Phase1_BPM_Swimlane.md` | Checkout process flow with 4 swim lanes | Recreate on Miro as your BPM diagram |
| `PO_Clarifying_Questions.md` | 20 questions grouped by domain | Consultation sessions with PO/mentor |
| `Team_Workflow.md` | Roles, git workflow, CI/CD, sprint plan | Team alignment on day 1 |
| This file | Your prep checklist | Tonight and tomorrow morning |

---

## DAY 1 MORNING — FIRST 30 MINUTES

### 5. Team Alignment (Do This Before Touching Code)

- [ ] Share the requirements doc and BPM with your team — get everyone on the same page
- [ ] Agree on roles (use `Team_Workflow.md` as starting point, adapt to who's actually on your team)
- [ ] Confirm tech stack with mentors/bootcamp — don't assume Java+Angular until they confirm
- [ ] Set up team communication channel (one channel, no scattered DMs)
- [ ] Create a Miro board with: Requirements section, BPM diagram, Kanban (To Do / In Progress / Review / Done)

### 6. First PO Consultation

- [ ] Lead with your top 5 questions from `PO_Clarifying_Questions.md`
- [ ] Record every answer in the doc
- [ ] Update requirements based on answers
- [ ] This is where you show the panelists you're a consulting team, not just coders

---

## ONCE TECH STACK IS CONFIRMED — Repo Setup (Benny's Job)

This is your lane. Whoever confirms the stack, you execute this within the hour:

- [ ] Create GitHub repo (private or org — whatever bootcamp says)
- [ ] Branch protection on `main` — no direct pushes, require PR + 1 review
- [ ] `.gitignore` for Java/Angular (use gitignore.io to generate)
- [ ] Scaffold backend (Spring Initializr if Java: Web, JPA, PostgreSQL, Validation, Security, Actuator)
- [ ] Scaffold frontend (`ng new comic-stock-frontend --routing --style=scss`)
- [ ] Basic CI pipeline (GitHub Actions: lint + test on PR)
- [ ] `README.md` — project name, how to run locally, team members
- [ ] First commit. Push. Share repo link with team.
- [ ] Verify every teammate can clone, build, and run locally

### If They Go .NET Instead:
- [ ] Same process, use `dotnet new webapi` instead of Spring Initializr
- [ ] Same Angular frontend
- [ ] Same CI pipeline (just change the build commands)

### If They Go Full JavaScript/TypeScript:
- [ ] Same process, use Express/Fastify + Next.js or Angular
- [ ] Same CI pipeline
- [ ] You're actually faster here — less boilerplate

**The repo setup pattern is identical regardless of stack. Only the build commands change.**

---

## WHAT NOT TO DO

- **Don't pre-build the app.** You don't know the stack, the DB provider, or even if they'll change the Phase 1 scope.
- **Don't over-design the architecture.** Start with the simplest thing that works. A controller, a service, a repository. That's it.
- **Don't go solo.** Your biggest asset tomorrow is showing up as a team lead who enables others, not a lone wolf who built everything overnight.
- **Don't memorize — understand.** If a panelist asks "why did you choose X?", you need a reason, not a recitation.
- **Don't stress about brilliance.** They want to see: "This team understands the problem, asked good questions, made decisions, and delivered a working checkout."

---

## MINDSET

You're not walking in as a student hoping to impress. You're walking in as a **consulting team** that:
1. Read the brief
2. Identified the ambiguities
3. Prepared questions for the client
4. Has a workflow ready to execute
5. Knows what "done" looks like (the success criteria)

That puts you ahead of 90% of teams who show up and start coding without understanding what they're building.
