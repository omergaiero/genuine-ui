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
- Decide where Zone 4 sits in `roadmap.md` (with Zone 3 in Phase 3, or later).
- Optionally fold the Q-numbering into `research-plan.md` so it's permanent.
- Pick a screen for the Track 2 agent test.

## Method notes (for reuse)
- Reddit scraping: built-in WebFetch/WebSearch are BLOCKED for reddit.com. Must use the `web-research-scraper` skill (scripts live in `capability and agent skills/capability skills/web-research-scraper/`, not the `~/.claude/skills/` copy which only has SKILL.md).
- Reddit search ranks by popularity: broad multi-keyword queries return generic high-upvote noise. **Tool-name-first queries** (e.g. just "Pendo") surface the actual relevant threads. This was the decisive fix.
- `ANTHROPIC_API_KEY` was NOT set in the terminal, so the skill's Haiku tagging/distillation steps were skipped; quotes were curated manually.

## Session Log
- 2026-05-27: Read all project docs. Ran Track 1 research → built `research-findings.csv`. Added Zone 4 to product brief. Ran web-research-scraper for Reddit (228 posts total across two runs); added 12 community quotes to CSV. Created this MEMORY.md.
