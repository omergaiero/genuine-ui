# Adaptive UI — Design Agent Test (Zone 1 + 2 Only)

---

## Layer 1 — Mock Data Schema

Two contrasting user profiles to demonstrate the adaptation delta.

### Profile A — Power User

```json
{
  "profile_id": "power_user",
  "user_profile": {
    "age_range": "25-35",
    "device": "desktop",
    "experience_level": "high",
    "use_case": "work",
    "language": "en"
  },
  "behavioral": {
    "sessions_total": 142,
    "avg_session_length_minutes": 38,
    "keyboard_shortcut_usage_rate": 0.72,
    "features_used": ["bulk_actions", "filters", "export", "search", "keyboard_nav"],
    "features_never_used": ["onboarding_tooltip", "help_center"],
    "search_queries_per_session": 0.4,
    "avg_reading_time_per_item_seconds": 3,
    "tooltip_skip_rate": 0.91,
    "navigation_pattern": "direct",
    "avg_actions_per_session": 47
  },
  "ugc": {
    "avg_message_length": "short",
    "tone": "terse",
    "uses_emoji": false,
    "vocabulary_complexity": "high",
    "uses_technical_terms": true
  }
}
```

### Profile B — Casual / Older User

```json
{
  "profile_id": "casual_older_user",
  "user_profile": {
    "age_range": "55+",
    "device": "desktop",
    "experience_level": "low",
    "use_case": "personal",
    "language": "en"
  },
  "behavioral": {
    "sessions_total": 14,
    "avg_session_length_minutes": 22,
    "keyboard_shortcut_usage_rate": 0.01,
    "features_used": ["search", "inbox"],
    "features_never_used": ["bulk_actions", "filters", "export", "keyboard_nav", "labels"],
    "search_queries_per_session": 3.8,
    "avg_reading_time_per_item_seconds": 18,
    "tooltip_skip_rate": 0.12,
    "navigation_pattern": "exploratory",
    "avg_actions_per_session": 8
  },
  "ugc": {
    "avg_message_length": "long",
    "tone": "formal",
    "uses_emoji": false,
    "vocabulary_complexity": "standard",
    "uses_technical_terms": false
  }
}
```

---

## Layer 2 — Adaptation Rules (Zone 1 + 2 Only)

### Zone 1 — Typography & Comfort

```yaml
rules:
  font_size:
    - if: user_profile.age_range in ["55+", "65+"]
      then: base_font_size = 18px, min_font_size = 16px
    - if: behavioral.avg_reading_time_per_item_seconds > 12
      then: base_font_size = 17px, line_height = 1.7
    - default: base_font_size = 14px, line_height = 1.5

  spacing:
    - if: user_profile.age_range in ["55+"]
      then: padding_multiplier = 1.4, increase_touch_targets = true
    - default: padding_multiplier = 1.0

  density:
    - if: behavioral.avg_session_length_minutes > 30 AND behavioral.avg_actions_per_session > 30
      then: density = compact, items_visible = 30
    - if: behavioral.avg_session_length_minutes < 15 OR user_profile.experience_level = low
      then: density = comfortable, items_visible = 8
    - default: density = default, items_visible = 15

  copy_tone:
    - if: ugc.tone = formal AND ugc.vocabulary_complexity = standard
      then: copy_style = clear_and_direct, avoid_jargon = true
    - if: ugc.uses_technical_terms = true AND user_profile.experience_level = high
      then: copy_style = terse, use_technical_labels = true
    - default: copy_style = friendly
```

### Zone 2 — Feature Visibility & Navigation

```yaml
rules:
  navigation:
    - if: user_profile.experience_level = low
      then: show_in_nav = ["inbox", "search", "compose"], collapse_rest = true
    - if: user_profile.experience_level = high
      then: show_in_nav = all, expand_labels = true
    - if: behavioral.features_never_used contains items AND behavioral.sessions_total > 10
      then: hide_from_primary_nav = behavioral.features_never_used

  shortcuts:
    - if: behavioral.keyboard_shortcut_usage_rate > 0.4
      then: show_keyboard_hints = true, shortcut_prominence = high
    - default: show_keyboard_hints = false

  advanced_features:
    - if: behavioral.features_used includes ["bulk_actions", "filters", "export"]
      then: surface_power_tools = true, show_in_toolbar = true
    - default: surface_power_tools = false, hide_in_overflow_menu = true

  search:
    - if: behavioral.search_queries_per_session > 2
      then: search_prominence = primary, search_size = large, autofocus = true
    - default: search_prominence = secondary
```

---

## Layer 3 — Design Agent Prompt

```
You are a product designer. Your job is to design screens for SaaS products.

For every screen you design, you will receive two inputs in addition to the feature brief:

1. A USER DATA object — behavioral and profile signals about the user.
2. AN ADAPTATION RULES set — a structured ruleset mapping signals to design decisions.

## Your process

Step 1 — Read the feature brief and understand the screen's goal.

Step 2 — Evaluate the user data against the adaptation rules.
For each rule that matches, note the design parameter it affects.

Step 3 — Apply Zone 1 rules first (typography, spacing, density, copy tone).
Then apply Zone 2 rules (navigation, feature visibility, shortcuts).

Step 4 — Design the screen with all matched rules applied.
Every design decision must be traceable to a rule or a design system default.

## Constraints

- Apply only Zone 1 and Zone 2 rules. Do not make structural layout changes beyond what the rules specify.
- When two rules conflict, apply the more conservative option.
- Stay within the product's existing design system. Do not invent new components.
- Changes must feel seamless — the screen should feel native, not patched.

## Output format

For each screen:
1. Figma frame — adapted design
2. Annotation layer — one annotation per applied rule, referencing the signal that triggered it
3. Profile summary — 3–5 bullet points: who is this design for and why does it look this way
```

---

## How to Run the Test

1. Pick one screen from the existing backlog.
2. Run the workflow twice — once with Profile A, once with Profile B.
3. Compare the two Figma outputs side by side.
4. Evaluate: are the differences meaningful and visually clear?
5. Note which rules produced strong output and which need refinement.

**What to look for:**
- Profile A → compact, dense, full nav, keyboard hints visible, power tools in toolbar
- Profile B → comfortable spacing, large text, simplified nav, large search bar, no shortcuts

If the two screens look nearly identical — the rules are not being applied correctly.
If the differences are clear and justified — the logic works.
