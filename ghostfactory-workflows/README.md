# GhostFactory Workflows

Public workflows, issue models and skills for AI-first product development.

Built for solo founders and small teams where issues are created by agents, not humans.

---

## What's here

### Workflows

Practical guides for running AI-assisted development workflows.

- **[Linear AI-First Issue Workflow](workflows/linear-ai-issue-workflow.md)**
  — How to use Linear as a control plane when Claude or another agent creates most of your issues. Covers lane/type model, Triage as checkpoint, hybrid model, priority rules and rollout steps.

### Skills

Reusable workflow modules for Claude (or any AI agent) working in Linear.

- **[Linear Skills Overview](skills/linear-skills-overview.md)**
  — Overview of operational skills for issue creation, triage, backlog hygiene and reporting.

### Templates

Ready-to-use issue templates for the GF_AOS lane/type model.

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
