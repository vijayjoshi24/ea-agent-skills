---
name: adr-writer
description: >
  Write Architecture Decision Records (ADRs) from design discussions, option
  comparisons, or technology choices. Activate whenever someone is making or
  documenting an architectural decision — including: "write an ADR", "document
  this decision", "we've decided to use X", "help me compare these options",
  "capture the rationale", "what are the trade-offs between", or when /decide
  is invoked. Also activates when a user describes a design choice they've made
  or are about to make, even without mentioning ADRs explicitly.
---

# ADR Writer

Capture architectural decisions as durable, structured ADRs. A decision not
documented is a decision that will be re-litigated — usually at the worst moment.

---

## Step 1 — Extract the Decision Context

From the user's description, identify:
- **The decision** — what was chosen or what needs to be chosen
- **The context** — what forces, constraints, and requirements drove this
- **The options** — what alternatives were considered (ask if not provided)
- **The deciders** — who made or will make this call
- **The consequences** — what becomes easier, harder, or different as a result

If the user is still deliberating (hasn't decided yet), run the options comparison
in Step 2 first, then write the ADR once they confirm a direction.

---

## Step 2 — Options Comparison (when deciding)

If the user has multiple options to evaluate, produce a comparison table:

| Criterion | Option A | Option B | Option C |
|---|---|---|---|
| Fit for use case | | | |
| Operational complexity | | | |
| Team skill match | | | |
| Cost | | | |
| Vendor/lock-in risk | | | |
| Time to implement | | | |
| **Verdict** | | | |

Score each cell: ✅ Strong / ⚠️ Acceptable / ❌ Weak  
End with a clear recommendation and one-sentence rationale.

---

## Step 3 — Write the ADR

Use this exact format. Do not skip sections.

```markdown
# ADR-NNN: {Concise title — what was decided, not just the topic}

**Date:** {YYYY-MM-DD}
**Status:** Proposed | Accepted | Deprecated | Superseded by ADR-NNN
**Deciders:** {names or roles}
**Tags:** {technology | pattern | platform | integration | security}

## Context

{What situation, constraint, or requirement makes this decision necessary?
What would happen if we made no decision? 2–4 sentences max.}

## Decision

{Active voice: "We will adopt / use / implement / reject..."
State the decision unambiguously in 1–2 sentences.}

## Options considered

| Option | Summary | Key trade-off |
|--------|---------|---------------|
| {A}    |         |               |
| {B}    |         |               |

## Consequences

### Positive
- {What becomes easier, faster, or safer}

### Negative
- {What becomes harder, more constrained, or more expensive}

### Risks and mitigations
| Risk | Likelihood | Mitigation |
|------|-----------|------------|

## Related decisions
- Supersedes: —
- Related to: —
- Enables: —
```

---

## Step 4 — File Placement Guidance

Tell the user where to save the ADR:

```
docs/decisions/ADR-NNN-{kebab-case-title}.md
```

Offer to auto-increment the ADR number if they share their existing ADR list.

---

## Quality Gate

- [ ] Title states the decision, not just the topic ("Use Azure Service Bus" not "Message Queue Selection")
- [ ] Context explains why a decision was needed, not just what options exist
- [ ] Decision is in active voice and unambiguous
- [ ] At least 2 options listed in the table, even if one was quickly eliminated
- [ ] Both positive and negative consequences present — no ADR has only upsides
- [ ] Status field is set
