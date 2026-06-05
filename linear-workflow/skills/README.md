# Linear Skills

Reusable **skills** for your Linear agent, working under the `<TEAM>` issue model. Add each one in `settings/ai-agents` → agent personalization → **Skills** (the section below guidance); you can also use them with any other AI agent.

Each skill is a single, self-contained task. They all assume:
- `Lane Now / Ready / Discovery / Later`
- `Type Bug / Feature / Discovery / Follow-up / Tech Debt / Chore`
- the ban on `triage:*` and the old `ready`
- the hybrid model: `Lane Ready` and `Lane Discovery` → Triage review, `Lane Later` → straight to the backlog

> General (non-Linear) skills — PRD breakdown, implementation spec, release notes, reporting — are in [`../../product-dev/skills/`](../../product-dev/skills/).

---

## Skills

| Skill | Purpose |
|---|---|
| [Create GF issues](create-gf-issues.md) | Creates new issues directly according to policy, template rules, and the lane/type model |
| [Triage issue](triage-issue.md) | Quick triage decision — 1× lane, 1× type, next step, priority |
| [Backlog grooming](backlog-grooming.md) | Verifies issue quality and readiness, surfaces missing info, risks, and dependencies |
| [Prioritize backlog item](prioritize-backlog-item.md) | Conservative priority based on impact, urgency, and risk |
| [Feature request to backlog](feature-request-to-backlog.md) | Turns an idea into a backlog issue, distinguishing Feature vs Discovery |
| [Bug report from notes](bug-report-from-notes.md) | Turns informal notes into a quality Bug issue |
| [Issue from informal input](issue-from-informal-input.md) | Turns fragmentary input into a properly structured and classified issue |

---

## Recommended use

**Session review** → `Create GF issues`, `Bug report from notes`, `Feature request to backlog`, `Issue from informal input`

**Backlog hygiene** → `Triage issue`, `Backlog grooming`, `Prioritize backlog item`

---

## Workflow architecture

- **Linear** = control plane: intake, triage, backlog, planning, execution handoff
- **Claude / agent** = operator: issue creation, initial classification, turning notes into structure
- **Human** = final decision: `Lane Now`, cycle selection, priority override, Triage review for `Lane Ready` and `Lane Discovery`

The most important layer is issue creation and sorting:

- **Templates** provide structure
- **Lane** says when and how the issue should be addressed
- **Type** says what kind of work it is
- **Triage** is a second check for issues with higher decision risk

The model is also portable to other AI-assisted teams, where issues are often created not by hand but through agents.
