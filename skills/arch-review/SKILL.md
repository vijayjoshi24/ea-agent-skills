---
name: arch-review
description: >
  Review an architecture submission, design proposal, or pattern choice against
  EA standards and produce structured feedback. Activate whenever someone wants
  architecture feedback, a design review, or ARB preparation — including: "review
  this architecture", "is this a good design", "what are the issues with", "prepare
  for ARB", "architecture critique", "check this against standards", "should we
  use this pattern", or when /review is invoked. Also activates when a user shares
  a design document, diagram description, or ADR and asks for feedback or approval
  recommendation.
---

# Architecture Review

Provide structured, evidence-based architecture review feedback. Reviews should
be honest, specific, and actionable — not just validating what the team already decided.

---

## Step 1 — Understand What's Being Reviewed

Identify:
- **What**: system, service, pattern, ADR, or full solution design
- **Stage**: early concept · detailed design · pre-ARB · post-implementation
- **Audience**: peer review · ARB · CTO · external audit
- **Constraints**: regulatory, legacy, budget, timeline (affect what's realistic to recommend)

---

## Step 2 — Score Across Seven Dimensions

Rate each dimension: ✅ Strong · ⚠️ Needs attention · ❌ Significant issue

| Dimension | What to assess |
|---|---|
| **Fitness for purpose** | Does the design actually solve the stated problem? Is it over- or under-engineered? |
| **Simplicity** | Is this the simplest design that would work? Are there unnecessary abstractions? |
| **Security** | Are controls proportionate to data sensitivity and threat model? Any obvious gaps? |
| **Resilience** | Single points of failure, retry/circuit-breaker patterns, failover strategy, data durability |
| **Operability** | Can it be deployed, monitored, scaled, and debugged in production? |
| **Standards alignment** | Does it follow enterprise technology standards and approved patterns? |
| **Decision quality** | Are key choices documented? Are trade-offs acknowledged? |

---

## Step 3 — Produce Findings

For each issue found, use this format:

```
[SEVERITY] {Dimension}: {concise issue title}
Finding: {what specifically is wrong or missing}
Impact: {what happens if this isn't addressed}
Recommendation: {specific action, not just "improve this"}
Effort: S (<1 day) | M (1 week) | L (1 sprint) | XL (>1 sprint)
```

Severity levels:
- **Critical** — blocks approval; must be resolved before proceeding
- **High** — should be resolved before implementation
- **Medium** — should be addressed in the next iteration
- **Low** — improvement opportunity, not blocking

---

## Step 4 — Deliver Structured Review

```markdown
## Architecture Review — {Subject}
**Date:** {date} | **Reviewer:** EA Agent | **Stage:** {stage}

### Scorecard
| Dimension | Rating | Summary |
|---|---|---|
| Fitness for purpose | ✅/⚠️/❌ | |
| Simplicity | | |
| Security | | |
| Resilience | | |
| Operability | | |
| Standards alignment | | |
| Decision quality | | |

### Findings ({N} total: {critical} critical, {high} high, {medium} medium, {low} low)
[findings in severity order]

### Strengths
[what the design does well — every review should acknowledge these]

### ARB Recommendation
- [ ] Approve
- [ ] Approve with conditions: {list conditions}
- [ ] Reject: {specific blockers to resolve before resubmission}

### Next review triggers
{What changes would warrant bringing this back for review?}
```

---

## Review Principles

**Be specific.** "The authentication design has a gap" is not useful. "The API Gateway
passes the raw JWT to downstream services without re-validating the signature, creating
a bypass risk if any internal service is compromised" is useful.

**Acknowledge what's good.** Architects who only receive criticism stop sharing early designs.

**Distinguish blockers from improvements.** Not everything needs to be fixed before proceeding.

**Avoid pattern snobbery.** A simpler pattern that works for this team's context beats
a theoretically superior one they can't operate.
