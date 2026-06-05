# Label Schema (template)

Official label set for the `<TEAM>` team in Linear. The canonical source of truth for label structure — skills, automations, and triage reference this.

The goal is a **clear, consistent, and enforceable** structure that enables:
- Effective triage
- Correct routing of AI-agent-created issues
- A clear distinction between work that is ready and work that requires a decision

---

## 1. Required labels

Every issue **must** have exactly **one Lane label** and **one Type label**.

### Lane labels — when / how the work will be handled

| Label | Color (suggested) | Meaning | Who sets it | Goes through Triage? |
|---|---|---|---|---|
| `Lane Now` | Red | Actively being worked on right now | **Human only** | No |
| `Lane Ready` | Green | Concrete, implementable, ready for planning | Agent | **Yes** |
| `Lane Discovery` | Yellow / Orange | Missing decision, scope, or validation | Agent | **Yes** |
| `Lane Later` | Gray | Valid work, but not now (low risk) | Agent | No — straight to backlog |

### Type labels — what kind of work it is

| Label | Color (suggested) | Use when |
|---|---|---|
| `Type Bug` | Red | Broken behavior, regression, wrong behavior |
| `Type Feature` | Purple | New capability or delivery item |
| `Type Discovery` | Yellow | Open question, audit, architecture decision, research |
| `Type Follow-up` | Blue | Follow-up after a review or completed issue |
| `Type Tech Debt` | Gray / Brown | Refactor, cleanup, hardening, maintainability — no open question |

> **Critical rule:**
> If an issue contains an **open question, audit, or decision** required before implementation → it **must** be `Type Discovery`.
> Even if it technically relates to cleanup or hardening.

---

## 2. Domain labels (optional)

Additional context labels. Not required — add only where they add value.

| Label | Color | Use when |
|---|---|---|
| `Frontend` | Blue | UI, components, client-side |
| `Backend` | Gray | Server-side, APIs, data layer |
| `infra` | Orange | Infrastructure, DevOps, deployment |
| `Security` | Red | Auth, access control, encryption, compliance |
| `Testing` | Green | Tests, test coverage, QA |
| `sdk` | Purple | SDK, integrations, external-facing code |
| `<DOMAIN_LABEL>` | — | Project-specific context |

> Example (GhostFactory): `ledger`, `otel`, `evals`, `runtime`, `observability`, `liveview`, `AI Agent`, `Tax & Legal`

Rules: a domain label is neither a lane nor a type. Max 3 per issue.

---

## 3. Forbidden labels

Do not use:
- `triage:*` as a classification model (Linear uses these internally)
- the old `ready`
- any label that duplicates a Lane or Type

---

## 4. How to create labels in Linear

1. Go to **Workspace settings → Labels**
2. Create labels per the tables above
3. Suggested colors:
   - `Lane Now` → strong red
   - `Lane Ready` → green
   - `Lane Discovery` → yellow / orange
   - `Lane Later` → neutral gray
   - Type labels → by meaning (red = Bug, yellow = Discovery, etc.)

---

## 5. Migrating existing labels

| Old label | New label | Action |
|---|---|---|
| `Bug` | `Type Bug` | Rename (optional) |
| `Feature` | `Type Feature` | Rename (optional) |
| `Improvement` | `Type Tech Debt` | Rename |
| Any "draft / proposal" label | `Type Discovery` | Rename |
| Other labels | — | Keep as domain labels if still useful |

---

## 6. Usage rules

- Every new issue (especially from an AI agent) must have **Lane + Type**.
- `Lane Now` may only be set by a **human**.
- Issues with `Lane Ready` or `Lane Discovery` should go through **Triage**.
- Domain labels are supplementary — not a replacement for lane or type.
