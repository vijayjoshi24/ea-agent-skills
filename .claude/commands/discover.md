# /discover

Analyse an existing system, codebase, or capability landscape to surface what's there,
what's missing, and what needs attention.

## When to use
Starting a new engagement, onboarding to an unfamiliar system, conducting an architecture
health check, or preparing for a transformation programme.

## What it produces

### For a codebase (Azure ADO repo)
- Tech debt score across 5 domains (Architecture, Code Quality, Security, Data & Integration, Testing)
- Prioritised findings with file-level evidence
- ADO-importable backlog of remediation items

### For a business landscape
- Business Capability Map with gap analysis
- Heatmap showing investment vs. strategic importance
- Application-to-capability mapping

## How to invoke

```
/discover
```

Then specify what you want to discover:

```
/discover codebase
org: myorg  project: MyProject  repo: my-service  branch: main
PAT: [your Azure DevOps PAT with Code:Read scope]
```

```
/discover capabilities
Here are our business functions: [paste list or description]
Map them against our application portfolio and show where we have gaps.
```

```
/discover landscape
We're a credit card issuer. Our key domains are: account origination,
servicing, payments, fraud, and digital channels. Help me map what
capabilities we need in each domain.
```

## Activates skills
- Codebase → `skills/tech-debt-scan/`
- Capabilities / landscape → `skills/capability-map/`
