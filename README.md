# GhostFactory Workflows

Public workflows, issue models and reusable AI skills for **AI-first product development** — built for solo founders and small teams where issues are created by agents, not humans.

> Templates give structure. Agent gives first classification. Triage gives the checkpoint. Human decides on active work.

---

## Categories

### 🎯 [Linear AI-First Workflow](linear-workflow/)

Using Linear as a control plane when Claude (or another agent) creates most of your issues. Stops the endless backlog-growth cycle with a strict lane/type model and Triage as a checkpoint.

- [Workflow guide](linear-workflow/workflow.md) — lane/type model, Triage, hybrid model, rollout
- [Setup](linear-workflow/setup/) — copy-paste configs mapped to Linear settings (AI agents, team workflow/triage)
- [Policy](linear-workflow/policy/) — canonical rules the skills reference
- [7 Linear skills](linear-workflow/skills/) — issue creation, triage, backlog hygiene
- [Issue templates](linear-workflow/templates/) — Bug · Feature · Discovery · Follow-up · Tech Debt

### 🧩 [Product-Dev Skills](product-dev/)

General, workflow-neutral skills for AI-assisted product development — not tied to any tracker.

- [6 product-dev skills](product-dev/skills/) — PRD → issue tree, implementation spec, release notes, reporting

---

## The lane/type model in short

**Lane** — every issue has exactly one:

| Lane | Meaning | Who sets it |
|---|---|---|
| Lane Now | Actively being worked on | Human only |
| Lane Ready | Concrete, ready for planning | Agent → Triage |
| Lane Discovery | Needs decision or scope clarity | Agent → Triage |
| Lane Later | Valid work, but not now | Agent → Backlog |

**Type** — every issue has exactly one: `Bug` · `Feature` · `Discovery` · `Follow-up` · `Tech Debt`

**Critical rule:** if an issue has an open question or needs a decision before implementation → `Type Discovery`, even if it looks like Tech Debt.

---

## Context

Built during development of [Span Chain](https://spanchain.dev) — a tamper-evident observability framework for AI agents. Part of the [GhostFactory .ART](https://ghostfactory.art) ecosystem.

> Agents Rule Tomorrow.

---

## License

MIT — use freely, adapt as needed. See [LICENSE](LICENSE).
