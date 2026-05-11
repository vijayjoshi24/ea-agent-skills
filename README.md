# EA Agent Skills

**Enterprise Architecture skills for AI agents.**

Skills encode the workflows, quality gates, and frameworks that senior Enterprise Architects
use when discovering, designing, deciding, reviewing, and communicating architecture.
Packaged so AI agents follow them consistently - across every engagement.

```
  DISCOVER        DESIGN          DECIDE          REVIEW          PRESENT
 ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐
 │ Inventory │  │ Diagram  │  │ Decide   │  │ Critique │  │ Narrate  │
 │ Landscape │  │ Model    │  │ Document │  │ Gate     │  │ Present  │
 └──────────┘  └──────────┘  └──────────┘  └──────────┘  └──────────┘
   /discover     /design       /decide       /review       /present
```

---

## Commands

5 slash commands that map to the EA lifecycle. Each activates the right skills automatically.

| What you're doing | Command | Key principle |
|---|---|---|
| Explore a system or landscape | `/discover` | See before you prescribe |
| Model a system visually | `/design` | Right level for the audience |
| Capture an architectural decision | `/decide` | Undocumented = re-litigated |
| Review an architecture submission | `/review` | Honest, specific, actionable |
| Present to stakeholders | `/present` | Business impact, not technical detail |

Skills also activate automatically based on what you're doing — describing a system
triggers `c4-diagram`, weighing technology options triggers `adr-writer`,
and so on.

---

## Quick Start

**Claude Code (recommended)**

```bash
git clone https://github.com/YOUR-USERNAME/ea-agent-skills
cd ea-agent-skills
claude .
```

**Paste into Claude.ai**

Open any skill's `SKILL.md` and paste it at the start of your conversation. The skill
activates immediately - no installation needed.

**Use a slash command**

```
/design
Our payment service has a React frontend, a .NET Core API, Azure SQL, 
and integrates with Stripe and Azure Service Bus.
```

```
/decide
We're choosing between GraphQL and REST for our new partner API.
Consumers are external partners with varying technical capabilities.
```

```
/review
[paste architecture description or design document]
```

---

## Skills

| Skill | What it does | Command |
|---|---|---|
| [`c4-diagram`](./skills/c4-diagram/) | Generate C4 Context, Container, and Component diagrams as interactive SVG | `/design` |
| [`adr-writer`](./skills/adr-writer/) | Write Architecture Decision Records with options comparison and consequence mapping | `/decide` |
| [`tech-debt-scan`](./skills/tech-debt-scan/) | Score an Azure ADO codebase for tech debt across 5 domains; produce ADO-importable backlog | `/discover` |
| [`capability-map`](./skills/capability-map/) | Build Business Capability Maps with gap analysis and investment heatmaps | `/discover`, `/present` |
| [`arch-review`](./skills/arch-review/) | Structured architecture review with 7-dimension scorecard and ARB recommendation | `/review` |

---

## How It Works

Each skill is a Markdown file that gives the agent deep, domain-specific instructions.
Skills use progressive loading — only what's needed gets read:

```
SKILL.md description    ← always active; agent reads this to decide relevance
SKILL.md body           ← loaded when the skill triggers; steps, output specs, quality gates  
references/             ← loaded on demand; notation guides, rubrics, archetypes
```

When you invoke a command or describe a task, the agent matches it to the right skill,
reads the instructions, and executes — following the same workflow a senior EA would use.

---

## Example Interactions

**Draw a C4 diagram**
```
/design
Our SaaS platform serves B2B customers. Users log in via Okta SSO, 
hit a Next.js frontend, which calls a FastAPI backend, which reads from 
Postgres and publishes events to Kafka. External: Stripe for billing, 
SendGrid for email.
```
→ Agent renders a C4 Context diagram. Click any element to drill into the Container level.

**Write an ADR**
```
/decide
We need to choose a messaging backbone for our new event-driven platform.
Options: Azure Service Bus vs Apache Kafka. We're Azure-native, 
team of 8 engineers, expecting 100k events/day at launch.
```
→ Agent produces an options comparison table, recommends Azure Service Bus with rationale,
then writes a complete ADR ready to commit.

**Scan for tech debt**
```
/discover codebase
org: myorg  project: PaymentService  repo: ps-api
PAT: [your PAT]
```
→ Agent fetches the repo structure and key files, scores 5 debt domains,
produces a scored report, a CSV for ADO import, and an executive summary.

**Review an architecture**
```
/review
We're proposing to use CQRS + Event Sourcing for our new account servicing API.
Read/write ratio is 80/20. Team size: 6 engineers. Expected load: 50k requests/day.
```
→ Agent scores 7 dimensions, flags over-engineering risk for this scale,
recommends a simpler CQRS-without-event-sourcing approach, and produces an ARB recommendation.

---

## Philosophy

**Architecture is communication.** The best architecture deliverable is the one the
right audience can understand and act on. These skills always match output to audience.

**Decisions are infrastructure.** Undocumented decisions are technical debt. Every
significant design choice surfaced in a session gets an ADR offer.

**Practitioner-first.** These skills come from real EA engagements — credit card
platforms, wealth management systems, agentic AI deployments. Not from certification
frameworks. The heuristics reflect how senior architects actually make decisions.

**Tool-connected.** Skills that connect to real systems (Azure DevOps, LeanIX, Azure)
produce outputs you can act on immediately. Generic analysis is a last resort.

---

## Contributing

EA practitioners at all levels are welcome. You don't need to be a developer —
domain knowledge and clear writing are the main requirements.

See [CONTRIBUTING.md](./CONTRIBUTING.md) for the full guide.

Fast paths:
- Add a new skill for an EA workflow you repeat constantly
- Add an archetype to an existing reference file
- Report a case where a skill produced wrong output
- Request a skill you wish existed

---

## About

Built by **Vijay Joshi** — Director of Enterprise Architecture with 20+ years across financial services (credit cards, wealth management, capital markets, retail banking).


---

## License

MIT — see [LICENSE](./LICENSE).
