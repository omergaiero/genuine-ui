# Product Roadmap — Adaptive UI

---

## Guiding Principle

Validate before building. Every phase gate requires evidence before moving to the next phase.

The MVP is not the SDK. The MVP is a demo that makes a buyer say "where do I sign."

---

## Phase 1 — Validate (Now)

**Goal:** prove the concept and the market before writing production code.

**Gate to Phase 2:** at least one buyer says "I would pay for this" after seeing the demo, AND research confirms the pain and persona.

### Track 1 — Market Research
Validate the pain, the persona, and the pricing signal.
See `research-plan.md` for full question set and sources.

Key questions to answer:
- Who owns UI iteration in a SaaS org — PM or Designer?
- What does it cost today (time + money) to adapt UI for different users?
- What are companies already paying for Pendo/Appcues/Optimizely?

### Track 2 — Agent Test
Test whether the adaptation logic produces meaningful visual differences.
See `design-agent-test.md` for profiles, rules, and agent prompt.

Process:
1. Pick one existing feature screen
2. Run design agent with Profile A (Power User)
3. Run design agent with Profile B (Casual/Older User)
4. Compare Figma outputs side by side
5. Assess: are differences meaningful and justified?

Success signal: two clearly different screens, each making sense for its user profile.

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

## Phase 2 — Build MVP (Post-Validation)

**Goal:** a real product that one paying customer uses.

**Gate to Phase 3:** one customer has integrated the SDK, is using the dashboard, and reports measurable improvement in activation or retention metrics.

### What gets built

**SDK (one-time engineering integration)**
- Thin JavaScript library
- Connects to existing design system tokens
- Captures behavioral events
- Reads from / writes to the adaptation engine

**Adaptation Engine**
- Zone 1 rules: typography, density, spacing, copy tone
- Zone 2 rules: navigation, feature visibility, shortcuts
- Signal ingestion from Amplitude / Mixpanel / Segment
- Per-user profile storage

**Dashboard (no-code operator tool)**
- Rule configuration interface
- Variant performance monitoring
- A/B comparison view
- User segment breakdown

**Scope constraints for MVP:**
- Zone 1 and Zone 2 only — Zone 3 comes later
- No Design Intelligence yet — adaptation engine first
- Single design system support — generic token schema

---

## Phase 3 — Expand

**Unlock these in order, based on demand signals from Phase 2 customers:**

### Zone 3 — Conscious Adaptation
The UX layer for data-backed suggestions to end users.
Requires: robust enough signal confidence to avoid false positives.
Includes: suggestion UI, accept/dismiss flow, performance tracking per accepted suggestion.

### Design Intelligence v1 — Insights Tab
Dashboard tab showing designers prioritized friction points with behavioral evidence.
Input: same behavioral data already collected.
Output: ranked list of hypotheses with supporting signals.

### Design Intelligence v2 — Screen Generation
Designer selects a hypothesis → system generates a screen addressing it.
Two outputs:
- Figma export — frame lands directly in designer's Figma file
- Live implementation — screen pushed as A/B variant without dev cycle

Closes the full loop: data → hypothesis → generated screen → test → back to data.

**Pre-condition for v2:** customer must have a defined design system (token-based). Works best with MUI, Tailwind, or a well-documented internal system.

### Proactive Alerts (later stage)
System pushes critical issues to the operator without them needing to open the dashboard.

Three levels:
| Level | Trigger | Example |
|---|---|---|
| Critical | Business metric impacted | Drop-off on key screen jumped from 20% to 45% |
| Warning | Pattern developing | Rage clicks on primary CTA tripled in one week |
| Insight | Improvement opportunity | Feature X discovered late by 80% of users |

**Why this is later:** requires solving the noise problem — distinguishing design issues from bugs, product changes, and seasonality. Alert fatigue kills the feature if this isn't right. Build only after the signal interpretation layer is mature.

---

## Design Intelligence Full Roadmap

| Stage | What it does | When |
|---|---|---|
| v1 | Insights tab — friction points with evidence | Phase 3 |
| v2 | Screen generation + Figma export + live A/B push | Phase 3 |
| v3 | Proactive alerts — push-based critical issue surfacing | Phase 3 (late) |

---

## The Moat Builds Over Time

Every customer added improves the intelligence layer for everyone:
- More signal patterns validated
- More adaptation rules refined
- More hypotheses confirmed or rejected

This is a network effect of intelligence. The product gets better with scale in a way competitors cannot easily replicate.
