# Research Plan — Adaptive UI

Qualitative research via literature review and social listening.
These are desk research questions — not interview questions.
Goal: validate pain, persona, and pricing before building anything.

---

## Research 1 — Persona Validation

**Core question: who actually owns UI iteration in a SaaS organization?**

The hypothesis is that a PM or Designer owns this day-to-day. But the pain and the budget may sit in different roles. This must be confirmed before deciding who to sell to and who to pitch.

### Literature Review Questions
- **Q1:** What roles in SaaS organizations own UI iteration responsibility post-launch?
- **Q2:** Is there documented tension or ambiguity between PM and Designer over UI decision ownership?
- **Q3:** What characterizes the Growth Designer or Product Designer role in mid-market SaaS?
- **Q4:** Who typically holds the budget for UX tooling in a 50–500 person company?

### Social Research Questions
- **Q5:** Do PMs or Designers discuss owning UI changes — or do they describe it as a shared/unclear responsibility?
- **Q6:** What do PM job descriptions say about UI optimization responsibility vs. Designer job descriptions?
- **Q7:** Is there documented frustration about not being able to make UI changes without engineering?

### Where to Look
- r/ProductManagement — search: "who owns UI changes", "PM vs designer", "shipping UI without eng"
- r/UXDesign — search: "PM keeps changing designs", "designer autonomy", "ownership"
- LinkedIn job postings — PM and Designer JDs at Series B/C SaaS companies
- Twitter/X — PM and designer community discussions on ownership
- Nielsen Norman Group — research on PM/designer collaboration

### Success Signal
A clear pattern: one role owns the pain AND has budget authority. Or a clear split that informs the sales approach.

---

## Research 2 — Pain Validation

**Core question: what does it cost today to adapt UI for different users, and what's broken about current solutions?**

### Literature Review Questions
- **Q8:** What is the documented cost of a UI change in a SaaS organization — engineering time, meetings, cycles?
- **Q9:** What is the average time between UX insight and production change?
- **Q10:** Is there research on the ROI of UX improvements on SaaS retention and activation?
- **Q11:** What are the documented limitations of A/B testing as a UX optimization approach?
- **Q12:** Why has adaptive UI remained a research concept and not become a mainstream product?

### Social Research Questions
- **Q13:** What do users of Pendo, Appcues, and Optimizely complain about in reviews?
- **Q14:** Do PMs discuss the frustration of long cycles between identifying a UX problem and fixing it?
- **Q15:** What workarounds do PMs and designers use when they can't get engineering time for UI changes?
- **Q16:** Is there documented dissatisfaction with manual A/B testing for UX?

### Where to Look
- G2 and Capterra reviews of Pendo, Appcues, Optimizely, LaunchDarkly — filter for negative reviews, look for patterns
- r/ProductManagement — search: "how long to ship UI change", "A/B testing frustration", "UX insight to production"
- Hacker News — search: "UX iteration", "personalization", "adaptive interface"
- LinkedIn posts by PMs — discussions on UX tooling and iteration speed
- ACM Digital Library / Google Scholar — "adaptive UI", "personalized interface", "UX iteration cost"
- Forrester / Gartner — reports on UX tooling in mid-market SaaS

### Success Signal
Documented evidence that:
1. The cycle from insight to UI change is slow and frustrating
2. Current tools don't actually change the UI — they guide or track
3. Companies feel this pain in their metrics (activation, retention)

---

## Research 3 — Pricing Signal

**Core question: what are companies already paying for this category, and what's the WTP?**

### Literature Review Questions
- **Q17:** What do Pendo, Appcues, Optimizely, and Dynamic Yield publicly charge for mid-market plans?
- **Q18:** What ROI metrics do SaaS companies use to justify UX tooling investments?
- **Q19:** What benchmarks exist for the cost of user churn vs. cost of retention in SaaS?
- **Q20:** What is the average engineering cost per UI change (developer time + overhead)?

### Social Research Questions
- **Q21:** Do PMs discuss their Pendo/Appcues pricing and whether it's worth it?
- **Q22:** What do users say about value-for-money on G2 reviews of these tools?
- **Q23:** Is there discussion about the cost of building UX personalization in-house vs. buying a tool?

### Where to Look
- G2 pricing pages + reviews: Pendo, Appcues, Optimizely, LaunchDarkly, VWO
- r/SaaS, r/startups — search: "how much Pendo", "UX tools budget", "Appcues worth it"
- LinkedIn — PMs discussing tooling budgets
- Transparent pricing pages: Appcues.com, Pendo.io, vwo.com
- SaaS benchmark reports: OpenView, Bessemer, Baremetrics

### Success Signal
A clear reference price range that mid-market SaaS companies are already paying for adjacent tools. This sets the pricing anchor.

---

## Research Execution Order

Start with **Research 2** (pain validation) — it's the most critical and easiest to find evidence for in reviews.

Then **Research 1** (persona) — job postings and community discussions give fast signal.

Then **Research 3** (pricing) — pricing pages + G2 reviews give concrete numbers.

---

## Sources Summary

| Goal | Academic | Industry | Community |
|---|---|---|---|
| Persona | ACM CHI, Nielsen Norman | LinkedIn job postings | r/UXDesign, r/ProductManagement |
| Pain | HCI journals, Forrester | G2/Capterra reviews of Pendo/Appcues | Hacker News, r/SaaS |
| Pricing | — | Gartner, pricing pages | r/startups, LinkedIn |
