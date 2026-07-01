# Strategy — Adaptive UI

---

## The Core Insight

Companies already have behavioral data on their users. They're not using it to improve the interface.

Every competitor in this space (Optimizely, LaunchDarkly, Dynamic Yield) requires the operator to manually define what changes. This product generates and refines adaptations automatically from behavioral signals — within the company's existing design system.

That is the strategic gap. That is what nobody else does.

---

## Why Now

The concept of adaptive UI has existed in HCI research for 20 years. It never became a product because inference was too expensive and too complex. That changed. LLMs dropped the cost and complexity by an order of magnitude. What was technically impossible in 2015 is straightforward in 2025.

---

## The Strategic Moat

The intelligence layer — not the UI layer.

Three things that are hard to replicate:
1. **What signals to collect** — not all data is equal. Knowing which signals actually predict friction takes trial and error across many users.
2. **How to interpret them** — rage clicks don't always mean affordance problems. Context determines meaning. The logic connecting signal to conclusion is the IP.
3. **What to do with the result** — validating that an adaptation solved the problem and didn't create a new one. The feedback loop that makes the system learning.

Every new customer improves the intelligence for everyone. This is a network effect of intelligence, not users. Hard to replicate.

---

## ICP — Ideal Customer Profile

**Company:**
- 50–500 employees
- Series A–C
- Dedicated product team (at least one PM + designer)
- Already using a behavioral analytics tool: Amplitude, Mixpanel, or Segment
- Not yet building this in-house

**Product:**
- B2B SaaS with daily or weekly usage
- Complex enough that onboarding matters
- User base with diverse roles and skill levels
- Minimum 500 MAU

**Pain signals to look for:**
- High early churn (first 30–60 days)
- Long time-to-value
- Support tickets about confusion
- NPS comments mentioning learning curve
- Already using Pendo or Appcues but dissatisfied with results

**Buyer:**
- Title: VP Product, Head of Growth, or CPO
- Measuring: activation rate, time-to-value, retention
- Frustrated by: the speed of the insight-to-fix cycle
- Currently trying: Pendo, Appcues, manual A/B testing

**Anti-ICP:**

| Segment | Why not |
|---|---|
| Pre-Series A | No budget, not enough data |
| Enterprise 1000+ | Long sales cycles, IT gatekeeping, builds in-house |
| Simple single-use products | No user diversity to adapt to |
| No analytics culture | No data to plug into |

---

## ICP by Data Maturity — [TO BE DISCUSSED]

> **Status:** proposal, not decided. Sharpens the ICP above by segmenting customers by their current data + design-system maturity, and defining what we do and do NOT do for each tier.

Customers arrive at different maturity points. The product serves two of them identically at the *product* level — the SDK, engine, and dashboard are the same. What differs is time-to-value.

| Tier | Customer has | What we do | Time to first value |
|---|---|---|---|
| **1 — Full** | DS + behavioral analytics | Plug in and adapt from day 1. Both Jobs (adapt UI + design intelligence) operational immediately. This is the ICP. | Days |
| **2 — Cold-start** | DS only (no analytics tool) | SDK becomes the data layer from day 1. Cold-start uses systematic exploration + best-practice defaults. Adaptations mature over weeks as behavioral signals accumulate. | Weeks |
| **3 — Not yet** | No DS (with or without data) | Anti-ICP. DS is the hard prerequisite — no tokens to vary means nothing to adapt. Come back when your team has one. | N/A |

**What we explicitly do NOT do:**
- Build design systems for customers (that's a months-long design engagement, not a SaaS product)
- Replace analytics tools like Amplitude/Mixpanel (our SDK captures what we need — but we're not competing on analytics depth)
- Serve customers without a design system at all (nothing to render adaptations against)

**Open questions to resolve before locking:**
- Is Tier 2 realistically sellable? Buyers without an analytics tool may not yet feel the pain that drives adoption.
- Should we source cold-start seed data from third-party providers (Clearbit, ZoomInfo) for *active signals* (role, industry, device)? Or keep it simple and rely on onboarding questions?
- Does "systematic exploration" (multi-armed bandit variants during cold-start) need a distinct dashboard mode, or does it live under the same rule-configuration UI?

---

## Competitive Position

| Competitor | What they do | The gap |
|---|---|---|
| Dynamic Yield | Content + recommendations personalization | Doesn't touch UI structure. Enterprise-only, $35k+/yr |
| Optimizely | A/B testing and manual UI variants | Variants are manually defined, not auto-generated |
| LaunchDarkly | Feature flags + experimentation | Requires dev work per change, no adaptive logic |
| Pendo | Analytics + in-app guidance | Guides users through existing UI, doesn't change it |
| Appcues | Onboarding flows by segment | Doesn't adapt the UI itself |

**Full competitive map:**

| | Personalizes UI structure | Auto-generated | Mid-market | No-code operator |
|---|---|---|---|---|
| Dynamic Yield | ✗ | Partial | ✗ | Partial |
| Optimizely | ✓ | ✗ | ✓ | Partial |
| LaunchDarkly | Partial | ✗ | ✓ | ✗ |
| Pendo | ✗ | ✗ | ✓ | ✓ |
| **This product** | **✓** | **✓** | **✓** | **✓** |

---

## Entry Point

**The pitch:** "You already have behavioral data on your users. You're not using it to improve the interface. We do that for you."

Target companies with:
- Established user bases (behavioral data already exists)
- An activation or retention problem they're actively trying to solve
- An existing analytics stack (Amplitude/Mixpanel/Segment)

**Not** an onboarding-first pitch. The value is strongest for existing users with rich behavioral history. Onboarding is supported from day one via active signals and general profiles — but it's not the selling point.

---

## The Problem Framing by Persona

| Persona | Pain | Current workaround | Why it fails |
|---|---|---|---|
| Buyer | One-size-fits-all UI hurts retention | A/B testing, periodic redesigns | Slow, expensive, full eng cycle every time |
| Operator | Every UI change needs engineering | Pendo, Appcues, tooltips | Surface-level, doesn't change the UI |
| End User | Interface doesn't match habits or skill | Manual settings, workarounds | Requires effort from the user |

---

## Pricing Direction (to be validated through research)

**Reference prices to investigate:**
- Pendo: ~$7k–$20k/yr for mid-market
- Appcues: ~$3k–$12k/yr
- Optimizely: $20k–$50k/yr
- Dynamic Yield: $35k+/yr (enterprise only)

**Hypothesis:** a mid-market SaaS company spending $8–15k/yr on Pendo and still dissatisfied is a natural buyer at a similar or slightly higher price point — if the value is demonstrably better.

**The ROI conversation:** frame in terms of retention improvement. If a $15k/yr tool improves 30-day retention by 5%, and average contract value is $500/yr, the math works quickly. Buyer already knows this math.

---

## Agent Experience — A Design Constraint, Not a Feature

By 2026, PMs and designers increasingly work *through* agents — Claude, Cursor, ChatGPT — rather than directly inside dashboards. This shifts what the product needs to be from "a pretty UI with an API bolted on" to "an API that happens to have a UI."

Two implications, both load-bearing:

**1. The dashboard is one client of the API, not the product itself.**
Every insight, hypothesis, rule, and adaptation outcome must be queryable through an MCP server or API. A designer asking Claude *"refine this screen — what's wrong with it?"* should resolve to a structured call into our system. The agent assembles the answer; we supply the intelligence. Build the API first; the dashboard later.

**2. Discovery happens through agents.**
When a PM asks Claude *"how should I change this screen to fit this user segment?"* — our system should be the tool Claude reaches for. That's distribution. Being agent-callable is the modern equivalent of being indexed in Google.

**Concrete consequence for MVP:** the dashboard and the MCP/API surface are built in parallel from day one. Not "ship dashboard, add API in v2." The contract between intelligence layer and consumer must be machine-readable from the start.

---

## The Three-Year View

In 2028, "adaptive UI" will be table stakes for serious SaaS products. The designer's job will shift from drawing screens to defining design systems and curating AI outputs. Continuous data-driven micro-adaptations will replace periodic big-bang redesigns. Most product work will be initiated and orchestrated through agents — the human curates, the agent executes.

This product is that infrastructure — built before the market has a name for it.
