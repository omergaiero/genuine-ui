# CLAUDE.md — Adaptive UI Project

## What This Is

An early-stage product being built by a solo founder with a design and product background.
The product is a white-label SDK + dashboard that adapts SaaS product UIs automatically to each user based on behavioral data.

This is not a design tool. It is an intelligence layer that sits between behavioral data and the rendered interface.

---

## Current Status

**Stage:** Pre-product. Concept validated in a strategy session. Now moving to three parallel tracks:

1. **Research** — validate personas and pain via literature review and social listening
2. **Agent test** — test the adaptation logic on an existing design agent workflow
3. **Gmail demo** — build a React proof-of-concept to show to potential buyers

No code has been written yet. No infrastructure exists yet.

---

## Documents in This Project

| File | What it contains |
|---|---|
| `CLAUDE.md` | This file. Start here. |
| `product-brief.md` | What the product is: the problem, solution, signal sources, adaptation zones, five logics, personas |
| `strategy.md` | ICP, competitive position, entry point, buyer, GTM direction, pricing signals |
| `roadmap.md` | Product roadmap across three phases + Design Intelligence roadmap |
| `research-plan.md` | Three research goals with specific questions and sources |
| `design-agent-test.md` | Agent test kit: two mock user profiles, Zone 1+2 rules, design agent system prompt |

---

## The One-Line Pitch

"You already have behavioral data on your users. You're not using it to improve the interface. We do that for you."

---

## The Core Constraint to Always Remember

**The guiding principle: additive before subtractive, reveal before relocate, suggest before change.**

Zone 1 and Zone 2 adaptations happen automatically and invisibly.
Zone 3 adaptations are never automatic — they are data-backed suggestions the user accepts or ignores.
This constraint protects against the "moving the cheese" failure mode that killed Microsoft Office's adaptive menus.

---

## Immediate Next Actions

**Track 1 — Research:**
Run the social listening queries in `research-plan.md`.
Start with: G2 reviews of Pendo/Appcues, r/ProductManagement, LinkedIn job postings for PM/Designer roles.
Goal: validate who owns the pain and what they're paying for it today.

**Track 2 — Agent test:**
Open `design-agent-test.md`.
Pick one existing feature screen.
Run the design agent twice — once with Profile A (Power User), once with Profile B (Casual/Older User).
Compare Figma outputs. If the two screens look meaningfully different and justified — the logic works.

**Track 3 — Gmail demo:**
Build a React app that shows an adapted Gmail inbox for three user profiles.
Components needed: OnboardingFlow (3 questions), GmailInbox (variant logic), ProfileSwitcher (for demo).
Purpose: show to a potential buyer. This converts "interesting" to "where do I sign."

---

## Open Questions to Resolve Through Research

- Does the PM or the Designer own this problem day-to-day in a SaaS org?
- What is the reference price — what are companies already paying for Pendo/Appcues/Optimizely?
- Which pain point is the stronger sales entry: activation metrics or ongoing retention?
