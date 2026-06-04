# Linear AI-First Workflow

Using Linear as a **control plane** when Claude (or another agent) creates most of your issues — not humans.

Built for solo founders and small teams where the backlog can otherwise grow faster than it shrinks: every session review spawns new issues, and the cycle never ends. This workflow stops that with a strict lane/type model plus Triage as a checkpoint.

---

## What's here

### Workflow guide

- **[Linear AI-First Issue Workflow](workflow.md)**
  — Full guide: lane/type model, Triage as checkpoint, the hybrid model, priority rules and a step-by-step rollout.

### Setup

- **[Setup — how to configure this in Linear](setup/)** — copy-paste-ready guidance/automation texts mapped to each Linear settings section (workspace AI agents, team workflow/triage).

### Policy

- **[Policy](policy/)** — canonical source of truth the skills reference: Final Issue Policy, Automation Spec, Template Selection Rules.

### Skills

Reusable single-task modules for Claude (or any AI agent) working in Linear.

- **[Linear Skills](skills/)** — 7 skills for issue creation, triage and backlog hygiene.

> General-purpose (non-Linear) skills live in [`../product-dev/skills/`](../product-dev/skills/).

### Templates

Ready-to-use issue templates for the lane/type model.

- [Bug](templates/bug.md)
- [Feature](templates/feature.md)
- [Discovery](templates/discovery.md)
- [Follow-up](templates/follow-up.md)
- [Tech Debt](templates/tech-debt.md)

---

## The model in one sentence

Templates give structure.
Agent gives first classification.
Triage gives checkpoint.
Human decides on active work.

---

## Key rules

**Lane system** — every issue has exactly one lane:

| Lane | Meaning | Who sets it |
|---|---|---|
| Lane Now | Actively being worked on | Human only |
| Lane Ready | Concrete, ready for planning | Agent → Triage |
| Lane Discovery | Needs decision or scope clarity | Agent → Triage |
| Lane Later | Valid work, but not now | Agent → Backlog |

**Type system** — every issue has exactly one type:

| Type | Use when |
|---|---|
| Bug | Broken behavior, regression |
| Feature | New capability |
| Discovery | Open question, audit, arch decision |
| Follow-up | Comes from review or completed issue |
| Tech Debt | Cleanup, refactor, hardening — no open question |

**Critical rule:** If an issue has an open question or requires a decision before implementation → `Type Discovery`. Even if it looks like Tech Debt.

---

## Context

Built during development of [Span Chain](https://spanchain.dev) — a tamper-evident observability framework for AI agents.

Part of the [GhostFactory .ART](https://ghostfactory.art) ecosystem.

> Agents Rule Tomorrow.

---

## License

MIT — use freely, adapt as needed.
