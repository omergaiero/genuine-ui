# MEMORY — Adaptive UI Project

## Current State (2026-05-27)

**Stage:** Phase 1 — Validate. Three parallel tracks: Research / Agent test / Gmail demo.

**Track 1 — Research: substantially done.**
- Output: `research-findings.csv` (56 findings) — columns: Quote, Source, Link, RQ, Q, Question.
- All research questions numbered: R1 (persona, Q1–Q7), R2 (pain, Q8–Q16), R3 (pricing, Q17–Q23). Numbering lives in the conversation, not yet in `research-plan.md`.
- Sources covered: G2/Capterra/TrustRadius reviews (via aggregator sites — G2 itself returns 403), Vendr/pricing pages, LinkedIn (titles only), and Reddit.
- Raw Reddit data: `reddit-research/combined.json` (151 posts) + `combined2.json` (77 posts).

**Key research learnings:**
- Strongest pain signal = engineering dependency (every tool: Appcues, Optimizely, LaunchDarkly) + slow insight-to-ship cycle.
- Pricing anchor confirmed: Pendo $25k–$132k/yr (avg ~$47k); Appcues median $15k/yr; community quote "$2k/quarter for 2k MAU."
- Best single quote (matches the product thesis exactly): r/PM "Faster way of iterating on in-app CTAs?" — waste of eng time to custom-code a simple design addition; Appcues/Pendo Guides lack flexibility.
- Ownership signal (R1): "Most PMs don't own the product. We coordinate it. Engineers decide what's technically realistic. Designers shape the experience."

**Track 2 — Agent test:** Not started. Kit is ready in `adaptive-ui-design-agent-v2.md` (Profiles A/B, Zone 1+2 rules, agent prompt). Needs a screen picked to run against.

**Track 3 — Gmail demo:** Not started.

**Product brief change this session:** Added **Zone 4 — User-Initiated Customization** to `product-brief.md` (user customizes directly; options curated by behavioral data, not a generic settings panel; explicit user intent overrides inferred system adaptation). Not yet reflected in `roadmap.md`.

## Open / Next
- Pick a screen for the Track 2 agent test (Zones 1+2). Plan a separate Figma prototype for Zones 3+4.
- Decide whether Zones 3+4 ship in Phase 2 MVP or get deferred to Phase 2.5 (depends on signal-confidence threshold).
- Apply research-plan refinement (still pending user approval): cut Q2/Q12/Q16, reclassify Q19/Q20 as stat lookups, add Q24 (agent usage), Q25 (qualitative aggregation), Q26 (diagnose-only product).
- `adaptive-ui-mapping.html` is now slightly out of sync with the brief — it shows Zones 1–3 only. The brief reflects Zone 4 as an overlay; the HTML doesn't. Update the HTML when convenient.

## Method notes (for reuse)
- Reddit scraping: built-in WebFetch/WebSearch are BLOCKED for reddit.com. Must use the `web-research-scraper` skill (scripts live in `capability and agent skills/capability skills/web-research-scraper/`, not the `~/.claude/skills/` copy which only has SKILL.md).
- Reddit search ranks by popularity: broad multi-keyword queries return generic high-upvote noise. **Tool-name-first queries** (e.g. just "Pendo") surface the actual relevant threads. This was the decisive fix.
- `ANTHROPIC_API_KEY` was NOT set in the terminal, so the skill's Haiku tagging/distillation steps were skipped; quotes were curated manually.

## Session Log
- 2026-05-27: Read all project docs. Ran Track 1 research → built `research-findings.csv`. Added Zone 4 to product brief. Ran web-research-scraper for Reddit (228 posts total across two runs); added 12 community quotes to CSV. Created this MEMORY.md.
- 2026-05-30: Baked Q1–Q23 numbering into `research-plan.md`. Major brief refactor: reorganized around "Two Jobs of UI Intelligence" (Job 1: Adapt UI to user / Job 2: Enhance product+design process). Added qualitative signals (support tickets, NPS, interviews, surveys) as fourth signal class. Made Adaptation Feedback Loop a first-class section. Added "UI-intelligence-driven A/B testing" to Job 2. Added "Agent Experience" strategic section to `strategy.md` — dashboard and MCP/API surface must ship in parallel from day one. Rewrote `roadmap.md`: Phase 2 = Job 1 only, built on two parallel tracks (Adaptation Engine + Dashboard-with-MCP-API). Job 2 = Phase 3. Zones 3+4 ship in Phase 2 if signal confidence allows; otherwise Phase 2.5. Qualitative-signal ingestion is Phase 3.
- 2026-06-10: Added `adaptive-ui-mapping.html` (visual matrix: Zones × Categories). Retired the Five Adaptation Logics (Proficiency / Friction / Frequency / Context / Preference) in the brief and replaced with the Three Categories framing (Physiological / Mental Model / Behavioral). Brief now includes a Category × Zone matrix with Zone 4 as an explicit user-initiated overlay. Framing: Zones = how/when, Categories = why. Added a clarification table in the brief that Zones 3 and 4 share the same change-set — they differ on initiator, trigger, UX surface, and signal value. Zone 4 is the stronger moat-builder (durable preferences > moment-of-suggestion choices).
