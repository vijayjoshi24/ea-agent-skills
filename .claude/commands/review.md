# /review

Review an architecture submission against EA standards and produce structured feedback.

## When to use
Pre-ARB (Architecture Review Board) submissions, peer design reviews, pattern
compliance checks, or post-implementation architecture audits.

## What it produces
- Structured review scorecard across key dimensions
- Specific findings with severity (Critical / High / Medium / Low)
- Recommendations with suggested remediation
- ARB recommendation: Approve / Approve with conditions / Reject

## How to invoke

```
/review
```

Then share what you want reviewed:

```
/review
[Paste architecture description, diagram description, or design doc]
```

```
/review adr
[Paste ADR text — review it for completeness and quality]
```

```
/review pattern
We're proposing to use CQRS + Event Sourcing for our payment service.
Is this appropriate given our scale (50k tx/day) and team size (6 engineers)?
```

## Review dimensions

| Dimension | What's checked |
|---|---|
| Fitness for purpose | Does it solve the stated problem? |
| Simplicity | Is it the simplest design that works? |
| Security | Are controls appropriate for the data/risk level? |
| Resilience | Single points of failure, retry patterns, circuit breakers |
| Operability | Can it be deployed, monitored, and supported? |
| Standards compliance | Does it follow enterprise technology standards? |
| Documentation | Is the decision and rationale captured? |

## Activates skill
`skills/arch-review/`
