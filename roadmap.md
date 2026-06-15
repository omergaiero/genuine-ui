# Product Roadmap — Adaptive UI

---

## Guiding Principles

Validate before building. Every phase gate requires evidence before moving to the next phase.

The MVP is not the SDK. The MVP is a demo that makes a buyer say "where do I sign."

**Job 1 (Adapt UI to user) is the first focus.** Job 2 (Enhance product/design process) is unlocked after Job 1 is proven in production. The dashboard and the MCP/API surface are built **in parallel from day one** — the API is the product, the dashboard is one client of it.

---

## Phase 1 — Validate (Now)

**Goal:** prove the concept and the market before writing production code.

**Gate to Phase 2:** at least one buyer says "I would pay for this" after seeing the demo, AND research confirms the pain and persona.

### Track 1 — Market Research
Validate the pain, the persona, and the pricing signal.
See `research-plan.md` for full question set; findings in `research-findings.csv`.

Key questions to answer:
- Who owns UI iteration in a SaaS org — PM or Designer?
- What does it cost today (time + money) to adapt UI for different users?
- What are companies already paying for Pendo/Appcues/Optimizely?

### Track 2 — Agent Test
Test whether the adaptation logic produces meaningful visual differences.

**Zones 1+2 (autonomous adaptation):** see `adaptive-ui-design-agent-v2.md` for profiles, rules, and agent prompt.
1. Pick one existing feature screen
2. Run design agent with Profile A (Power User)
3. Run design agent with Profile B (Casual/Older User)
4. Compare Figma outputs side by side
5. Assess: are differences meaningful and justified?

**Zones 3+4 (user-approved adaptation):** separate test — a Figma prototype showing:
- Zone 3: the suggestion modal ("we noticed X, want to try Y?") → accept/reject → resulting changed screen
- Zone 4: the customization menu, with options scoped to a specific user profile (proves it's not a generic settings panel)

Success signal: for Zones 1+2 — two clearly different screens, each justified. For Zones 3+4 — a coherent UX flow a designer can show a buyer.

### Track 3 — Gmail Demo
Build a React proof-of-concept showing Gmail inbox adapted for three user profiles.

**Three profiles:**
- Power User (dense, full nav, shortcuts visible, compact toolbar)
- Casual User (comfortable spacing, simplified nav, basic toolbar)
- Older User (large font, high contrast, minimal nav, large search bar)

**What to build:**
- OnboardingFlow — 3 questions that determine the profile
- GmailInbox — renders differently based on active profile
- ProfileSwitcher — lets demo viewers switch between profiles live

**Stack:** React, mock email data (20 items), 3 layout variants.

**Purpose:** show to a potential buyer. This is what converts "interesting" to "where do I sign."

---

## Phase 2 — Build MVP (Job 1, with API-first dashboard)

**Goal:** ship Job 1 — Adapt UI to user — as a real product that one paying customer uses.

**Gate to Phase 3:** one customer has integrated the SDK, is using the dashboard via UI *and* via agent, and reports measurable improvement in activation or retention metrics.

### Two parallel build tracks

#### Track A — Job 1 Adaptation Engine

**SDK (one-time engineering integration)**
- Thin JavaScript library
- Connects to existing design system tokens
- Captures behavioral events
- Reads from / writes to the adaptation engine

**Adaptation Engine — Zones 1+2 first (autonomous)**
- Zone 1 rules: typography, density, spacing, copy tone
- Zone 2 rules: navigation, feature visibility, shortcuts
- Signal ingestion from Amplitude / Mixpanel / Segment
- Per-user profile storage
- **Feedback loop instrumentation** — every adaptation logged with the behavioral delta that followed; failed adaptations auto-reverted

**Adaptation Engine — Zones 3+4 (user-approved), if signal confidence allows in MVP; otherwise Phase 2.5**
- Zone 3 suggestion UI, accept/dismiss flow, per-suggestion performance tracking
- Zone 4 user-customization menu, options scoped by user profile
- Accept/reject and customization choices feed back into rule confidence

#### Track B — Dashboard + MCP/API surface (parallel, from day one)

**API/MCP surface (built first, dashboard built against it)**
- Every adaptation rule, user profile, hypothesis, and outcome queryable via API and MCP
- Machine-readable contracts for all dashboard data
- Auth, rate limiting, audit log

**Dashboard (one client of the API)**
- Rule configuration interface
- Variant performance monitoring
- A/B comparison view
- User segment breakdown
- Per-user adaptation log (for debugging and support)

**Why API first:** PMs and designers increasingly work through agents (Claude, Cursor, ChatGPT). If a PM asks Claude *"how should I change this screen for power users?"*, our system should be the tool Claude reaches for. Building the API as an afterthought forces a rewrite later.

### Scope constraints for MVP
- **Job 1 only.** Job 2 (Design Intelligence + UI-intel-driven A/B testing) is Phase 3.
- Active + behavioral + UGC signals only. Qualitative signal ingestion (support tickets, NPS, interviews) is Phase 3.
- Single design system support — generic token schema.

---

## Phase 2.5 — Complete Job 1 (only if Zones 3+4 deferred from Phase 2)

If Phase 2 shipped Zones 1+2 only, this phase closes Job 1 by adding the user-approved layer.

- Zone 3 suggestion UI and accept/dismiss flow
- Zone 4 user-customization menu (profile-scoped options)
- Strengthened feedback loop — Zone 3 accept/reject and Zone 4 customizations are the highest-quality training signals the system gets

**Why Zones 3+4 matter even more than Zones 1+2 for the moat:** every accept/reject is a labeled training example. The intelligence layer compounds faster here than from passive behavioral inference alone.

---

## Phase 3 — Expand to Job 2

Unlock these in order, based on demand signals from Phase 2 customers.

### Job 2a — Design-intelligence suggestions (Insights Tab)
Dashboard tab + API endpoint showing designers prioritized friction hypotheses with behavioral evidence.
- Input: same behavioral data already collected, now augmented with qualitative signals
- Output: ranked list of hypotheses with supporting signals — both for humans and for agents to consume

### Job 2b — UI-intelligence-driven A/B testing
The system proposes — or fully runs — A/B tests where the variant is generated from the same adaptation logic that powers Job 1.
- **Manual mode first:** designer reviews hypothesis, picks variant approach, system instruments and runs the test
- **Automated mode later:** system selects high-confidence hypotheses, generates variants, runs tests, pushes winner to the design system
- Two output paths:
  - Figma export — frame lands directly in designer's Figma file
  - Live implementation — variant pushed as A/B without a dev cycle

This closes the full loop: signal → hypothesis → generated variant → test → live UI → back to signal.

**Pre-condition for live implementation path:** customer must have a defined design system (token-based). Works best with MUI, Tailwind, or a well-documented internal system.

### Qualitative signal ingestion
Expand the intelligence layer beyond clicks.
- Support tickets and chat transcripts
- NPS comments and CSAT free-text
- User-interview transcripts
- Survey responses
- Sales / CS call notes

LLM-based extraction turns unstructured text into structured signals fed into the same engine. This is the moat expansion that competitors (limited to click data) cannot easily follow.

### Proactive Alerts (later stage)
System pushes critical issues to the operator without them needing to open the dashboard.

| Level | Trigger | Example |
|---|---|---|
| Critical | Business metric impacted | Drop-off on key screen jumped from 20% to 45% |
| Warning | Pattern developing | Rage clicks on primary CTA tripled in one week |
| Insight | Improvement opportunity | Feature X discovered late by 80% of users |

**Why this is later:** requires solving the noise problem — distinguishing design issues from bugs, product changes, and seasonality. Alert fatigue kills the feature if this isn't right.

---

## Job 2 Full Roadmap

| Stage | What it does | When |
|---|---|---|
| Job 2a v1 | Insights tab — friction hypotheses with evidence, served via UI and MCP | Phase 3 |
| Job 2b v1 | Manual UI-intel-driven A/B testing (designer-curated variants) | Phase 3 |
| Job 2b v2 | Automated UI-intel-driven A/B testing (system-generated variants, Figma + live push) | Phase 3 |
| Qualitative ingestion | Support tickets, NPS, interview transcripts → structured signals | Phase 3 |
| Proactive alerts | Push-based critical issue surfacing | Phase 3 (late) |

---

## The Moat Builds Over Time

Every customer added improves the intelligence layer for everyone:
- More signal patterns validated across products
- More adaptation rules refined
- More Zone 3 accept/reject decisions = more labeled training data
- More Zone 4 customizations = highest-quality "the default doesn't fit me" signals
- More qualitative inputs (Phase 3) widen the moat further — competitors limited to click data can't triangulate

This is a network effect of intelligence — not users. The product gets better with scale in a way competitors cannot easily replicate.
