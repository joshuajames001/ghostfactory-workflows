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

| Label | Color | Meaning | Who sets it | Goes through Triage? |
|---|---|---|---|---|
| `Lane Now` | `#DC2626` (red) | Actively being worked on right now | **Human only** | No |
| `Lane Ready` | `#2563EB` (blue) | Concrete, implementable, ready for planning | Agent | **Yes** |
| `Lane Discovery` | `#7C3AED` (purple) | Missing decision, scope, or validation | Agent | **Yes** |
| `Lane Later` | `#6B7280` (gray) | Valid work, but not now (low risk) | Agent | No — straight to backlog |

### Type labels — what kind of work it is

| Label | Color | Use when |
|---|---|---|
| `Type Bug` | `#DC2626` (red) | Broken behavior, regression, wrong behavior |
| `Type Feature` | `#2563EB` (blue) | New capability or delivery item |
| `Type Discovery` | `#7C3AED` (purple) | Open question, audit, architecture decision, research |
| `Type Follow-up` | `#D97706` (amber) | Follow-up after a review or completed issue |
| `Type Tech Debt` | `#6B7280` (gray) | Refactor, cleanup, hardening, maintainability — no open question |
| `Type Chore` | `#9CA3AF` (light gray) | Routine maintenance, dependency bumps, config, tooling/CI, setup/ops — no direct user value and no code-quality change |

> **Critical rule:**
> If an issue contains an **open question, audit, or decision** required before implementation → it **must** be `Type Discovery`.
> Even if it technically relates to cleanup or hardening.

> **Tech Debt vs Chore:**
> Improves the quality of existing code (refactor, cleanup, hardening) → `Type Tech Debt`.
> Pure upkeep with no user value and no quality change (deps, config, CI, setup, ops) → `Type Chore`.

---

## 2. Domain labels (optional)

Additional context labels. Not required — add only where they add value.

| Label | Color | Use when |
|---|---|---|
| `Frontend` | `#10B981` (green) | UI, components, client-side |
| `Backend` | `#0EA5E9` (sky) | Server-side, APIs, data layer |
| `infra` | `#6B7280` (gray) | Infrastructure, DevOps, deployment |
| `Security` | `#EF4444` (red) | Auth, access control, encryption, compliance |
| `Testing` | `#10B981` (green) | Tests, test coverage, QA |
| `sdk` | `#0EA5E9` (sky) | SDK, integrations, external-facing code |
| `<DOMAIN_LABEL>` | — | Project-specific context |

> Example (GhostFactory): `ledger`, `otel`, `evals`, `runtime`, `observability`, `liveview`, `AI Agent`, `Tax & Legal`

Rules: a domain label is neither a lane nor a type. Max 3 per issue.

---

## 3. Status labels (situational)

Optional, situational labels. Like domain labels, they are **not** a Lane or a Type and do **not** satisfy the "one Lane + one Type" requirement. Add them during triage or grooming when they apply.

| Label | Color | Use when |
|---|---|---|
| `blocked` | `#EF4444` (red) | Blocked by a decision, dependency, or missing input |
| `needs refinement` | `#F59E0B` (amber) | Right direction, but not enough detail to start work |

---

## 4. Forbidden labels

Do not use:
- `triage:*` as a classification model (Linear uses these internally)
- the old `ready`
- any label that duplicates a Lane or Type

---

## 5. How to create labels in Linear

1. Go to **Workspace settings → Labels**
2. Create labels per the tables above, using the exact hex colors
3. Quick reference:
   - Lanes: `Lane Now` `#DC2626` · `Lane Ready` `#2563EB` · `Lane Discovery` `#7C3AED` · `Lane Later` `#6B7280`
   - Types: `Type Bug` `#DC2626` · `Type Feature` `#2563EB` · `Type Discovery` `#7C3AED` · `Type Follow-up` `#D97706` · `Type Tech Debt` `#6B7280` · `Type Chore` `#9CA3AF`
   - Status: `blocked` `#EF4444` · `needs refinement` `#F59E0B`

> These hex values match `assets/labels.svg` and `setup/mcp-workspace-setup.md` — keep all three in sync.

---

## 6. Migrating existing labels

| Old label | New label | Action |
|---|---|---|
| `Bug` | `Type Bug` | Rename (optional) |
| `Feature` | `Type Feature` | Rename (optional) |
| `Improvement` | `Type Tech Debt` | Rename |
| Any "draft / proposal" label | `Type Discovery` | Rename |
| Other labels | — | Keep as domain labels if still useful |

---

## 7. Usage rules

- Every new issue (especially from an AI agent) must have **Lane + Type**.
- `Lane Now` may only be set by a **human**.
- Issues with `Lane Ready` or `Lane Discovery` should go through **Triage**.
- Domain and status labels are supplementary — not a replacement for lane or type.
