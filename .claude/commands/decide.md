# /decide

Capture an architectural decision as a formal ADR (Architecture Decision Record).

## When to use
Any time a significant design choice is made — technology selection, pattern adoption,
build-vs-buy, integration approach, platform strategy. Decisions not documented
are decisions that will be re-litigated.

## What it produces
- A complete ADR in standard format: Title, Status, Context, Decision, Consequences
- Optional: trade-off comparison table across the evaluated options
- Optional: link map to related ADRs (supersedes / superseded-by)

## How to invoke

```
/decide
```

Then describe the decision. Examples:

```
/decide
We're choosing between Azure Service Bus and Kafka for our event backbone.
The system needs to handle 50k events/day, we're an Azure-native shop,
and the team has limited Kafka ops experience.
```

```
/decide
We've decided to adopt the Strangler Fig pattern to migrate our monolith.
Capture the rationale, alternatives we considered, and the consequences.
```

## Output format

```markdown
# ADR-{NNN}: {Title}

**Date:** {date}  
**Status:** Proposed | Accepted | Deprecated | Superseded  
**Deciders:** {who made this decision}

## Context
{What forces are at play? What problem are we solving?}

## Decision
{What was decided, in active voice: "We will..."}

## Options considered
| Option | Pros | Cons | Fit |
|--------|------|------|-----|

## Consequences
### Positive
### Negative  
### Risks and mitigations

## Related decisions
```

## Activates skill
`skills/adr-writer/`
