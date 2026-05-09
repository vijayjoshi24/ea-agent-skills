---
name: capability-map
description: >
  Build Business Capability Maps with gap analysis, investment heatmaps, and
  application-to-capability mapping. Activate whenever someone mentions business
  capabilities, capability models, strategic planning, investment prioritisation,
  or wants to understand what a business does vs what technology supports it —
  including: "build a capability map", "what capabilities do we need", "map our
  applications to business functions", "capability gap analysis", "where should
  we invest", "what capabilities support this strategy", or when /discover landscape
  or /present is invoked. Also activates when a user describes business domains
  and asks what they should be building or where the gaps are.
---

# Capability Map

Build a Business Capability Map that shows what the organisation does, how well
technology supports each capability, and where to invest next.

---

## Core Concept

A capability describes **what** a business does, not **how** or **who** does it.
"Payment Processing" is a capability. "Stripe integration" is an implementation.
Capabilities are stable; implementations change.

---

## Step 1 — Define the Capability Model

From the user's description, build a three-level hierarchy:

```
Level 1 — Domain        (e.g. "Customer Management")
  Level 2 — Capability  (e.g. "Customer Onboarding")
    Level 3 — Sub-cap   (e.g. "Identity Verification")
```

For common industries, use the reference archetypes in `references/archetypes.md`
as a starting point, then adapt to what the user describes.

Aim for 5–8 Level 1 domains, 3–6 Level 2 capabilities per domain. Go to Level 3
only when the user needs that granularity.

---

## Step 2 — Score Each Capability (when requested)

For each Level 2 capability, ask the user to rate (or infer from context):

| Dimension | Scale | Meaning |
|---|---|---|
| Strategic importance | 1–5 | How critical to business strategy? |
| Current maturity | 1–5 | How well does current tech support this? |
| Investment priority | High / Medium / Low | Where should investment go? |

Gap = Strategic importance minus Current maturity. Capabilities with Gap ≥ 2 are priority investment areas.

---

## Step 3 — Map Applications to Capabilities

If the user provides an application list, map each application to the capabilities it supports:

```
| Application | Capabilities supported | Coverage |
|---|---|---|
| Salesforce CRM | Customer Onboarding, Account Management | Strong |
| Legacy Mainframe | Payment Processing, Reconciliation | Weak — modernisation candidate |
```

Surface: gaps (capabilities with no application support) · overlaps (multiple apps
doing the same thing) · modernisation candidates (critical capability, weak app support).

---

## Step 4 — Render Outputs

### A — Visual Heatmap

Use `show_widget` to render an interactive capability map:
- Grid layout: domains as columns, capabilities as rows
- Cell colour: green (well-supported) · amber (partial) · red (gap) · grey (not assessed)
- Click any cell → `sendPrompt('Tell me more about the {capability} capability gap')`

### B — Gap Analysis Table

```markdown
| Capability | Strategic importance | Current maturity | Gap | Priority |
|---|---|---|---|---|
| Identity Verification | 5 | 2 | 3 | HIGH |
```

### C — Investment Narrative (for /present)

150–200 word business case framing: "Our {N} highest-priority capability gaps are
in {domains}. Closing these gaps enables {business outcomes}. The recommended
investment sequence is..."

---

## Reference Files

- `references/archetypes.md` — pre-built capability models for financial services (credit card, wealth management), SaaS, and retail. Use as starting point, adapt to the user's context.
