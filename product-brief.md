# Product Brief — Adaptive UI

---

## The Problem

SaaS products serve one interface to all users — regardless of skill level, usage habits, role, or context. This creates friction for everyone except the average user the product was designed for.

Companies know this. They do A/B testing, build onboarding flows, write tooltip copy. But every change requires a full design-engineering cycle. By the time a fix ships, the insight is stale. The gap between "we know there's a problem" and "we fixed it" is measured in weeks or quarters.

---

## The Solution

A thin SDK that engineering integrates once, connected to the company's existing design system, behavioral data, and qualitative inputs. From that point on, a dashboard gives the product team full control to define adaptation logic, see design-intelligence insights, and monitor results — no further engineering required.

The same intelligence layer powers two distinct jobs.

---

## The Two Jobs of UI Intelligence

| Job | Who it serves | What it does |
|---|---|---|
| **1. Adapt UI to user** | The end user | Renders the same screen differently for each user — automatically (Zones 1+2) or with their approval (Zones 3+4) |
| **2. Enhance product/design process** | The PM / designer | Surfaces friction hypotheses and proposes/runs A/B tests based on UI intelligence, before a designer redraws a screen |

Both jobs are powered by the same intelligence layer (signals + interpretation + feedback loop). The cost of building that layer is amortized across both — and every customer that uses one improves the layer for the other.

---

## Job 1 — Adapt UI to User

### Autonomous adaptation (Zones 1 + 2)

#### Zone 1 — Invisible
User never notices. Feels like the product was built for them.
- Font size, line height, preview length
- Density and spacing
- Color weight and contrast
- Copy tone

#### Zone 2 — Additive
Applied between sessions, never mid-session. Reveals and adds — never removes or relocates.
- Surface shortcuts for power users
- Reveal advanced features to proficient users
- Hide features the user has never touched after many sessions

### User-approved adaptation (Zones 3 + 4)

#### Zone 3 — Conscious Adaptation
Never automatic. System presents a data-backed suggestion with reasoning. User accepts or ignores.
- Navigation item reordering
- Interaction model changes (drag vs. click)
- Layout structure changes

Format: *"We noticed [behavior]. We think [change] would work better for you. Want to try it?"*
Frequency rule: suggest only when signal is strong, max once per defined time window.

#### Zone 4 — User-Initiated Customization
The user pulls the lever directly. Where Zone 3 is the system suggesting a change, Zone 4 is the user actively customizing their own interface.

The differentiator from a generic settings panel: the customization options are curated by behavioral data, not a fixed list of toggles. A power user is offered different controls than a casual user — the system only surfaces options relevant to that user's profile.

- User-adjustable density, layout, and visible features
- Options scoped by the user's behavioral profile, not a universal menu
- The system bounds what can be customized to protect against self-inflicted friction

Zone 3 = the product says *"try this."* Zone 4 = the user says *"give me this."*

**Same change-set, different paths.** Zones 3 and 4 act on largely the same elements — navigation, layout, feature visibility, density. What separates them isn't *what* changes, it's the path the change takes:

| | Zone 3 — System push | Zone 4 — User pull |
|---|---|---|
| Initiator | System | User |
| Trigger | Signal threshold reached + frequency rule passes | User opens customization menu anytime |
| UX surface | One-shot suggestion modal / banner | Persistent customization screen |
| Signal value back | "Yes/no on this specific recommendation, in this moment" | "I prefer X in general" — broader, more stable |

Zone 4 is the stronger moat-builder. Explicit user preferences ("give me dense, hide labels") are higher-quality labeled signals than per-suggestion accept/reject — they speak to durable taste, not a single-moment choice.

### Guiding principles for Job 1

**Additive before subtractive, reveal before relocate, suggest before change.**

User-initiated changes (Zone 4) override system adaptations — explicit user intent always wins over inferred intent.

---

## Job 2 — Enhance Product/Design Process

The same intelligence layer, pointed at a different consumer: the designer and PM, before they redraw a screen.

### 2a. Design-intelligence suggestions for screen refining

When a designer is planning a redesign, the system surfaces data-backed hypotheses about where friction lives — built from the same signals that power Job 1.

**Honest framing: data-backed design hypotheses, not design recommendations.**
The system tells you WHERE the problem is with high confidence. The design solution remains the designer's judgment.

#### Signal → Hypothesis Mapping

| Signal | Source | Hypothesis |
|---|---|---|
| Rage clicks on element | Hotjar, FullStory | Affordance problem |
| Dead clicks | FullStory, LogRocket | Visual hierarchy misleading |
| Feature searched repeatedly | Any analytics | Navigation / IA mismatch |
| Feature never used | Pendo, Amplitude | Discoverability problem |
| High funnel drop-off | Amplitude, Mixpanel | Friction or cognitive overload |
| High time on task | Amplitude | Too complex, simplify |
| Scroll depth cutoff | Hotjar | Important content below fold |
| Repeated form errors | LogRocket, Sentry | Labeling or validation flow broken |
| Negative sentiment cluster | Support tickets, NPS | Emerging UX issue not yet visible in clicks |
| Interview / survey theme | User research | Confirmed problem with qualitative weight |

### 2b. UI-intelligence-driven A/B testing

When a hypothesis is strong enough to act on, the system can propose — or fully run — an A/B test, with the variant generated from the same adaptation logic that powers Zones 1–4.

Two modes:
- **Manual:** designer reviews the hypothesis, picks the variant approach, system instruments and runs the test.
- **Automated:** the system selects high-confidence hypotheses, generates a variant, runs the test, and pushes the winner to the design system — closing the full loop from signal → test → live UI.

This is what eliminates the "weeks-to-ship-a-UX-fix" cycle the problem statement opens with.

---

## The Intelligence Layer (powers both jobs)

### Signal Sources

The system pulls from four signal classes. Each class compounds the value of the others — qualitative gives meaning to behavioral; behavioral validates qualitative.

#### Active signals (Day 1)
What the user explicitly tells us.
Onboarding answers, self-reported experience level, role, device type, use case.

#### Behavioral signals (accumulate over time)
What the user shows through interaction.
Click patterns, feature usage breadth, reading time, hover/hesitation, session length, shortcut usage, scroll speed, error clicks, back-button frequency, tooltip skip rate, search queries per session.
Sources: Amplitude, Mixpanel, Segment, FullStory, Hotjar, LogRocket, or raw events.

#### UGC signals (Day 1, in products with text input)
How the user writes inside the product.
Writing style (formal vs. casual), message length, punctuation precision, vocabulary complexity, technical-term use, emoji usage.

#### Qualitative signals (the moat expansion)
What the user says outside the product, and what research has uncovered.
- Support tickets and chat transcripts
- NPS comments and CSAT free-text
- User-interview transcripts
- Survey responses
- Sales / CS call notes

Why this matters: a user complaining in a support ticket *and* clicking back-button four times on the same screen is a triangulated signal worth 10× either alone. Competitors that only ingest clicks can't see this. LLMs make extracting structure from this unstructured text newly possible.

### Adaptation Feedback Loop

The system learns from every user's response to every adaptation — and improves continuously.

- **Zone 1 + 2 (autonomous):** validated by behavioral deltas after the change (did engagement go up? did the user keep using the feature?). Failed adaptations are auto-reverted.
- **Zone 3 (user-approved):** every accept or reject is a labeled signal. Accept = the system's hypothesis was right. Reject = update the user's profile to suppress similar suggestions and refine the rule.
- **Zone 4 (user-customized):** what users choose to customize themselves is the highest-quality signal of all — it's an explicit "the default doesn't fit me." That choice updates the rule confidence for users with similar profiles.

Every adaptation produces a labeled training example. Every customer's loop improves the rule library for every other customer. This is the network effect of intelligence.

### Data richness over time

| User stage | Adaptation basis | Precision |
|---|---|---|
| New user | Active signals + general profiles | Moderate |
| Developing user | Emerging behavioral patterns | Rising |
| Established user | Full behavioral + qualitative profile | High |

The product's value compounds with time. Longer customer = better product for their users. Retention mechanic is built in.

### The Three Categories — Why a User Needs Different UI

**Zones answer *how and when* a change is applied. Categories answer *why* it's needed.** Every adaptation has both.

| Category | Question it answers | Source | When available |
|---|---|---|---|
| **Physiological** | What do their physical & cognitive traits require? | Active signals — age, device, accessibility settings | Day 1 |
| **Mental Model** | What conventions do they bring from other tools? | Onboarding answers, UGC vocabulary, early interaction patterns | Day 1 |
| **Behavioral** | What have we learned from their usage *here*? | Passive signals — usage patterns inside this product | Accumulates over time |

#### Category × Zone matrix

|  | Zone 1 — Invisible | Zone 2 — Additive | Zone 3 — Conscious |
|---|---|---|---|
| **Physiological** | Font size, line height, spacing, contrast, density, touch target size | — | — |
| **Mental Model** | Copy tone, terminology, label style | Interaction patterns, shortcut visibility, familiar conventions | Navigation structure, IA reordering, layout conventions |
| **Behavioral** | Preview length, search prominence, density refinement | Feature visibility, shortcut surfacing, hide unused items, action ordering | Layout suggestion, interaction model, nav restructure |

**Zone 4 overlay (user-initiated):** The user can pull the lever on any of the above where the system permits. The options surfaced are scoped to their profile — not a generic settings panel. A user who already has dense layouts inferred via Behavioral signals won't see "increase density" as a customization choice; the system reads their context and offers only what's relevant.

#### How to read the matrix

- **By row (Category → Zone):** Physiological needs are handled quietly in Zone 1 only. Mental Model spans all three zones. Behavioral grows in depth as data accumulates — subtle Zone 1 tuning at first, Zone 3 proposals once the profile is rich.
- **By column (Zone → Category):** Zone 1 is driven by Physiology + early signals (Day 1). Zone 2 is driven by Mental Model + Behavioral patterns (needs some data). Zone 3 needs strong, consistent Mental Model and Behavioral signals before suggesting.

### Zone 1 Signal Mapping

| Adaptation | Active signals | Behavioral signals | UGC signals |
|---|---|---|---|
| Font size | Age, accessibility settings | Browser zoom, slow reading time, error clicks | — |
| Density | Device type, display preference | Scroll speed, session length, scan behavior | — |
| Spacing | — | Misclicks, long hover before clicking | — |
| Contrast | — | Time of day, OS accessibility settings | — |
| Preview length | Use case (work/personal) | Reading time per item | — |
| Copy tone | Language, locale, experience level | — | Writing style, formality, sentence length, emoji |

### Zone 2 Signal Mapping

| Adaptation | Active signals | Behavioral signals |
|---|---|---|
| Reveal advanced features | Self-reported experience, role | Shortcut usage, interaction speed, tooltip skips |
| Surface shortcuts | — | Repeated sequences, same features every session |
| Hide unused features | — | Never clicked after many sessions, zero return visits |
| Feature discovery | — | Explores independently vs. stays on known paths |

---

## Personas

### The Buyer — VP Product / CPO
Owns retention and activation metrics. Will pay when ROI is clear.
**Primary need:** measurable improvement in user metrics without high engineering cost.

### The Operator — PM / Designer
Works the dashboard day-to-day. Defines rules, monitors variants, reviews design-intelligence insights, decides which A/B tests to run.
**Primary need:** fewer engineering handoffs, faster iteration, data-backed decisions.

### The End User
Doesn't know or care about adaptive UI. Just wants no friction.
**Primary need:** things work the way they expect, without configuring anything.
