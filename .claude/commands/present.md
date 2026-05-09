# /present

Transform technical architecture into stakeholder-ready communication — executive
narratives, board slides, business cases, and one-pagers.

## When to use
Preparing for CIO/CTO briefings, board presentations, investment proposals,
programme steering committees, or vendor strategy communications.

## What it produces
- Executive narrative (200–400 words, business language, no jargon)
- Slide structure outline (titles + key point per slide)
- One-pager summary with problem, approach, outcomes, ask
- Business case framing (investment, expected value, risk of inaction)

## How to invoke

```
/present
```

Then describe what needs presenting:

```
/present
Summarise our cloud migration strategy for the board. Key points:
we're moving from on-prem to Azure over 3 years, starting with
dev/test environments, estimated cost saving of $2M by year 3,
main risk is skills gap in the infrastructure team.
```

```
/present exec
Turn this tech debt assessment into a 5-minute CIO briefing.
[Paste assessment or summary]
```

```
/present slides
Create a slide structure for our EA strategy presentation.
Audience: EVP Technology and business unit leaders.
```

## Tone principles
- Lead with business impact, not technical detail
- Frame debt and risk in terms of delivery velocity and cost
- Use outcomes language: "enables", "reduces", "accelerates", "protects"
- One idea per slide — never more than 5 bullet points on any slide

## Activates skill
`skills/capability-map/` (for landscape views) + inline presentation logic
