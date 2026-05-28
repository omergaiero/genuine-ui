# Product Brief — Adaptive UI

---

## The Problem

SaaS products serve one interface to all users — regardless of skill level, usage habits, role, or context. This creates friction for everyone except the average user the product was designed for.

Companies know this. They do A/B testing, build onboarding flows, write tooltip copy. But every change requires a full design-engineering cycle. By the time a fix ships, the insight is stale. The gap between "we know there's a problem" and "we fixed it" is measured in weeks or quarters.

---

## The Solution

A thin SDK that engineering integrates once, connected to the company's existing design system and behavioral data (Amplitude, Mixpanel, Segment, or raw events). From that point on, a dashboard gives the product team full control to define adaptation logic and monitor results — no further engineering required.

The system adapts the UI continuously and automatically. The same screen, the same goals — rendered differently for different users.

---

## What Changes (Adaptation Scope)

### Zone 1 — Invisible
User never notices. Feels like the product was built for them.
- Font size, line height, preview length
- Density and spacing
- Color weight and contrast
- Copy tone

### Zone 2 — Additive
Applied between sessions, never mid-session. Reveals and adds — never removes or relocates.
- Surface shortcuts for power users
- Reveal advanced features to proficient users
- Hide features the user has never touched after many sessions

### Zone 3 — Conscious Adaptation
Never automatic. System presents a data-backed suggestion with reasoning. User accepts or ignores.
- Navigation item reordering
- Interaction model changes (drag vs. click)
- Layout structure changes

Format: *"We noticed [behavior]. We think [change] would work better for you. Want to try it?"*
Frequency rule: suggest only when signal is strong, max once per defined time window.

### Zone 4 — User-Initiated Customization
The user pulls the lever directly. Where Zone 3 is the system suggesting a change, Zone 4 is the user actively customizing their own interface.

The differentiator from a generic settings panel: the customization options are curated by behavioral data, not a fixed list of toggles. A power user is offered different controls than a casual user — the system only surfaces options relevant to that user's profile and within what it allows.

- User-adjustable density, layout, and visible features
- Options scoped by the user's behavioral profile, not a universal menu
- The system bounds what can be customized to protect against self-inflicted friction

Zone 3 = the product says *"try this."* Zone 4 = the user says *"give me this."*

**Guiding principle: additive before subtractive, reveal before relocate, suggest before change.**
User-initiated changes (Zone 4) override system adaptations — explicit user intent always wins over inferred intent.

---

## Signal Sources

### Active signals (Day 1)
What the user explicitly tells us.
Onboarding answers, self-reported experience level, role, device type, use case.

### Passive behavioral signals (Accumulate over time)
What the user shows through interaction.
Click patterns, feature usage breadth, reading time, hover/hesitation, session length, shortcut usage, scroll speed, error clicks, back button frequency, tooltip skip rate, search queries per session.

### UGC signals (Day 1, in products with text input)
How the user writes inside the product.
Writing style (formal vs. casual), message length, punctuation precision, vocabulary complexity, use of technical terms, emoji usage.

**Data richness over time:**

| User stage | Adaptation basis | Precision |
|---|---|---|
| New user | Active signals + general profiles | Moderate |
| Developing user | Emerging behavioral patterns | Rising |
| Established user | Full behavioral profile | High |

The product's value compounds with time. Longer customer = better product for their users. Retention mechanic is built in.

---

## The Five Adaptation Logics

| Logic | Key signals | What adapts |
|---|---|---|
| **Proficiency** | Interaction speed, shortcut usage, feature breadth, tooltip skips | Density, visible options, progressive disclosure |
| **Friction** | Hover without click, back button, abandonment, repeated attempts | Step complexity, guidance, number of options |
| **Frequency** | Repeated action sequences, most-visited screens | Navigation order, shortcut prominence |
| **Context** | Time of day, device, session length | Layout mode, density, focused vs. exploratory |
| **Preference** | Filter use, search vs. browse, changed settings | Search prominence, content order, interaction model |

---

## Zone 1 Signal Mapping

| Adaptation | Active signals | Passive signals | UGC signals |
|---|---|---|---|
| Font size | Age, accessibility settings | Browser zoom, slow reading time, error clicks | — |
| Density | Device type, display preference | Scroll speed, session length, scan behavior | — |
| Spacing | — | Misclicks, long hover before clicking | — |
| Contrast | — | Time of day, OS accessibility settings | — |
| Preview length | Use case (work/personal) | Reading time per item | — |
| Copy tone | Language, locale, experience level | — | Writing style, formality, sentence length, emoji |

## Zone 2 Signal Mapping

| Adaptation | Active signals | Passive signals |
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
Works the dashboard day-to-day. Defines rules, monitors variants, makes decisions.
**Primary need:** fewer engineering handoffs, faster iteration, data-backed decisions.

### The End User
Doesn't know or care about adaptive UI. Just wants no friction.
**Primary need:** things work the way they expect, without configuring anything.

---

## Design Intelligence (Secondary Feature)

A capability built on top of the same behavioral data layer. When a designer is planning a redesign, the system surfaces data-backed hypotheses about friction points.

**Honest framing: data-backed design hypotheses, not design recommendations.**
The system tells you WHERE the problem is with high confidence.
The design solution remains the designer's judgment.

### Signal → Hypothesis Mapping

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

**Pre-condition:** requires a behavioral analytics tool connected (Amplitude, Mixpanel, Hotjar, or equivalent).
