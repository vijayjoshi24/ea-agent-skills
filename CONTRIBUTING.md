# Contributing to EA Agent Skills

Skills get better when people with real EA experience contribute their knowledge.
You don't need to write code — clear Markdown and domain expertise are what matter.

---

## Ways to Contribute

| Type | What | Effort |
|---|---|---|
| New skill | A new EA workflow, packaged as a SKILL.md | Medium |
| New command | A slash command that maps to a workflow | Low |
| New archetype | A reference example for a system type | Low |
| Skill improvement | Better steps, sharper quality gates, fixed output | Low |
| Bug report | Skill produced wrong output | Very low |
| Skill request | Describe a skill you wish existed | Very low |

---

## Skill Format

```
skills/your-skill-name/
├── SKILL.md              ← required; keep under 500 lines
└── references/           ← optional; loaded on demand
    ├── rubric.md
    └── archetypes.md
```

**SKILL.md frontmatter**
```yaml
---
name: skill-name
description: >
  What it does AND when it triggers. Include 5+ specific phrases,
  including implicit triggers (e.g. "also activates when a user pastes
  a file tree and asks what to fix, even without mentioning tech debt").
---
```

**Writing rules**
- Numbered, imperative steps — not prose paragraphs
- Define output format precisely (column names, word counts, label formats)
- Include a quality gate checklist
- Include error handling for common failure modes
- Stay under 500 lines; move depth to `references/`

---

## Submitting a Skill

1. Check `skills/` and open issues — avoid duplicating something in progress
2. Open a [skill request issue](../../issues/new?template=skill-request.md) for larger skills
3. Fork → create `skills/your-skill-name/` → write `SKILL.md`
4. Test against 3+ realistic prompts and document results in your PR
5. PR title: `feat: add {skill-name}`

**PR checklist**
- [ ] `name:` and `description:` frontmatter present
- [ ] 5+ trigger phrases in description
- [ ] Steps are numbered and imperative
- [ ] Output format defined with at least one example
- [ ] Quality gate / checklist present
- [ ] Error handling section present
- [ ] Tested against 3+ prompts
- [ ] Under 500 lines
- [ ] No org-specific data, credentials, or proprietary content

---

## Adding a Slash Command

Commands live in `.claude/commands/`. Each is a Markdown file that describes:
- When to use the command
- Example invocations with natural language
- Which skill it activates

PR title: `feat: add /{command-name} command`
