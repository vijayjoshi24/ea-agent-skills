---
name: tech-debt-scan
description: >
  Scan an Azure DevOps repository or pasted codebase description to quantify
  technical debt by domain and severity. Activate whenever someone mentions tech
  debt, code quality, architecture health, modernisation readiness, or asks what
  needs fixing in a codebase — including: "analyze my repo for tech debt",
  "score our architecture debt", "what's the state of our code", "find gaps in
  our codebase", "modernisation assessment", "what should we fix first", or when
  /discover codebase is invoked. Also activates when a user pastes a file tree,
  dependency list, or code snippet and asks for an assessment.
---

# Tech Debt Scan

Analyse a codebase for technical debt across five domains. Produce a scored report,
a prioritised remediation backlog, and an executive summary.

Read `references/scoring-rubric.md` before scoring any domain.

---

## Step 1 — Gather Inputs

Ask for:
1. **ADO connection** — org / project / repo / branch + PAT (`Code: Read` scope)
2. **Tech stack hint** (optional) — e.g. ".NET 8, React, Azure SQL"
3. **Scope** (optional) — specific folders or modules to focus on

If the user pastes a file tree, dependency file, or code samples instead, work from that.

---

## Step 2 — Fetch Repository Structure

```
GET https://dev.azure.com/{org}/{project}/_apis/git/repositories/{repo}/items
    ?scopePath=/&recursionLevel=Full&api-version=7.1
Authorization: Basic base64(:{PAT})
```

Prioritise fetching content for: `*.csproj` · `package.json` · `pom.xml` ·
`requirements.txt` · `Dockerfile` · `azure-pipelines.yml` · `appsettings*.json` ·
`.env*` · `README.md` · `Program.cs` / `app.py` / `index.js` (entry points) ·
up to 10 source files across different modules · any `*test*` folders.

Skip binary files. Cap at ~30 file reads for large repos.

---

## Step 3 — Score Five Domains

Read `references/scoring-rubric.md` for the full signal list and weights.

Domains (0–100, higher = more debt):
1. **Architecture & Design** — structure, coupling, EOL frameworks, missing IaC
2. **Code Quality & Complexity** — god classes, missing error handling, TODOs, no linting
3. **Security & Compliance** — secrets in code, no secrets management, HTTP endpoints, missing SAST
4. **Data & Integration** — hardcoded URLs, no retry patterns, mixed data access, no API spec
5. **Testing & Observability** — no tests, no logging framework, no health checks, no pipeline test step

Per domain, produce:
- Score (0–100) + severity: `Low 0–30` / `Medium 31–60` / `High 61–80` / `Critical 81–100`
- Top 3 findings with file path evidence
- Confidence: `High` (direct evidence) / `Medium` (structural inference) / `Low` (inferred from absence)

**Overall Debt Index** = weighted average: Architecture 25% · Code Quality 20% · Security 25% · Data 15% · Testing 15%

---

## Step 4 — Three Outputs

### A — Scored Domain Report

```markdown
## Tech Debt Scan — {repo} ({date})

| Domain | Score | Severity | Confidence |
|--------|-------|----------|------------|
| Architecture & Design | | | |
| Code Quality | | | |
| Security & Compliance | | | |
| Data & Integration | | | |
| Testing & Observability | | | |
| **Overall Debt Index** | | | |

### Key findings (top 3 per domain)
[file-referenced, specific, actionable]

### Immediate actions (cross-domain top 5)
[prioritised by risk × effort]
```

### B — ADO Backlog CSV (copy-paste importable)

```
Title,Work Item Type,Priority,Tags,Description,Effort
[TechDebt][Security] Remove hardcoded credentials from config,Bug,1,tech-debt;security,...,8
```

Rules: Critical/security → `Bug` Priority 1; others → `Task` Priority 2–4.
Tags always include `tech-debt`. Effort: Critical=8, High=5, Medium=3, Low=1.

### C — Executive Summary (150–250 words)

Business-language narrative for a VP/CTO. Lead with Overall Debt Index and
delivery velocity impact. Call out the 1–2 highest-risk domains. Three-horizon
remediation view: Quick wins · Mid-term · Strategic. Close with recommended
engineering investment percentage.

---

## Error Handling

- **401/403**: Verify PAT has `Code: Read` scope and org/project/repo names are exact
- **Repo >500 files**: Analyse structure + config files only; flag confidence as Medium
- **No test files found**: Auto-score Testing domain ≥65 (High); absence is the finding
- **No live repo access**: Ask user to run `git ls-files` and paste the output

---

## Reference Files

- `references/scoring-rubric.md` — full signal checklist and weights per domain
