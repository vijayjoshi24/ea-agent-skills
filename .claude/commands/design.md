# /design

Model a system's architecture as a C4 diagram.

## When to use
Describe a system, paste a list of services, share a README, or just say what you're building.
The agent will extract the key elements and render the right C4 level for your audience.

## What it produces
- Context diagram (for business/executive audiences)
- Container diagram (for architects and engineers)
- Component diagram (for development teams)
- Interactive SVG with clickable drill-down between levels

## How to invoke

```
/design
```

Then describe your system in natural language. Examples:

```
/design
Our credit card platform has a React portal, a .NET API, Azure SQL, 
and integrates with Visa for payment processing and Azure AD for auth.
```

```
/design context
Show how our SaaS platform fits into the wider business ecosystem.
```

```
/design container
Zoom into the payment service — it has a REST API, a background worker, 
a Postgres database, and publishes to a Kafka topic.
```

## Levels

Append a level hint to control zoom depth:
- `/design context` — system boundary, users, external systems
- `/design container` — deployable units inside the system
- `/design component` — structural building blocks inside one container

Default (no level): agent starts at Context and offers to drill down.

## Activates skill
`skills/c4-diagram/`
