---
name: c4-diagram
description: >
  Generate C4 model architecture diagrams — Context, Container, Component — as
  interactive rendered SVG visuals. Activate whenever someone wants to diagram,
  visualise, or document a system's architecture, including: "draw a C4 diagram",
  "show me the architecture of", "create a context diagram", "container diagram for",
  "visualise how this system works", "map out the services", "architecture diagram",
  or when a user describes a system and asks how it fits together. Also activates
  when /design is invoked, or when a user pastes a system description and asks
  for an architecture view — even without mentioning C4 or diagrams explicitly.
---

# C4 Diagram

Generate interactive C4 model diagrams at the right zoom level for your audience.
Read `references/notation.md` before rendering any diagram.

---

## The Four Levels

| Level | Audience | Shows |
|---|---|---|
| 1 — Context | Business, executives | The system + its users + external systems |
| 2 — Container | Architects, tech leads | Deployable units inside the system |
| 3 — Component | Engineering teams | Structural building blocks inside one container |
| 4 — Code | Developers | Class/interface level — skip unless explicitly requested |

---

## Step 1 — Determine Level and Extract Elements

If the user hasn't specified a level, default to **Context** first.

Extract from the user's description:

**Context:** system in scope · people/actors · external systems · relationships  
**Container:** containers (with technology) · external systems they call · relationships with protocols  
**Component:** which container to zoom into · components (with pattern/technology) · internal + external relationships  

State any assumptions you make (e.g. "Assumed: auth is delegated to the API Gateway").

---

## Step 2 — Render the Diagram

Use the `show_widget` visualiser. Follow `references/notation.md` exactly for:
- Shapes and colours per element type
- Label format: name · [type] · description (one sentence)
- Relationship arrows: one direction, labelled with intent + technology
- Title: `{Level} Diagram — {System Name}`
- Legend in bottom-right corner

Make every element clickable to drill down:
- Container in Context → `sendPrompt('Draw the Container diagram for {system}')`
- Container in Container → `sendPrompt('Draw the Component diagram for {container}')`
- External system → `sendPrompt('Explain the {system} integration')`

Max 10 elements per diagram. If more exist, scope to the most relevant and note omissions.

---

## Step 3 — Quality Gate

Before delivering, verify:
- [ ] Title present
- [ ] Every element: name + [type] + description
- [ ] Every relationship: directional arrow + intent label
- [ ] External systems visually distinct (grey)
- [ ] People distinct from systems
- [ ] Legend present
- [ ] ≤10 elements

---

## Step 4 — Offer Navigation

After Context → offer Container  
After Container → offer Component for a specific container  
After Component → offer Structurizr DSL export or ArchiMate equivalent

---

## Reference Files

- `references/notation.md` — canonical colours, shapes, label rules per level. Read before every render.
- `references/archetypes.md` — worked examples for FS, SaaS, agentic AI, microservices.
