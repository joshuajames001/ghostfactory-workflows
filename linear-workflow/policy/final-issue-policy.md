# Final Issue Policy (template)

Final operational policy for the `<TEAM>` team. The canonical source of truth for issue classification — both skills and automations refer back to this.

## 1. Mandatory classification axes
Every new issue should have:
- **1× Lane**
- **1× Type**
- optionally **0–3 domain labels**
- priority

## 2. Lane labels
Use only: `Lane Now`, `Lane Ready`, `Lane Discovery`, `Lane Later`

### Rules
- an issue must not have more than one lane label
- `Lane Now` is never set automatically
- when in doubt: `Lane Discovery` (not `Lane Ready`)

### Meaning
- `Lane Now` — actively being worked on right now
- `Lane Ready` — concrete, implementable, ready for planning; before going to the backlog, run through Triage review
- `Lane Discovery` — needs a decision, validation, or breakdown; run through Triage
- `Lane Later` — valid work, but not now; can go straight to the backlog

## 3. Type labels
Use only: `Type Bug`, `Type Feature`, `Type Discovery`, `Type Follow-up`, `Type Tech Debt`, `Type Chore`

### Rules
- an issue must not be without a type, nor have more than one type

### Meaning
- `Type Bug` — bug, regression, incorrect behavior
- `Type Feature` — new capability or value delivery
- `Type Discovery` — the goal is a decision, not implementation
- `Type Follow-up` — follows up on completed work, a review, or a previous issue
- `Type Tech Debt` — refactor, cleanup, infra hardening, maintainability (improves existing code quality)
- `Type Chore` — routine maintenance, dependency bumps, config, tooling/CI, setup/ops; no user value and no code-quality change

## 4. Domain labels
Team-level, used only where they make sense.
- **Common:** `Frontend`, `Backend`, `infra`, `Security`, `Testing`, `sdk`
- **Project-specific:** `<DOMAIN_LABEL>` depending on the project

> Example (GhostFactory) — observability project: `ledger`, `otel`, `evals`, `runtime`, `observability`, `liveview`, `scale`, `versioning`

Rules: a domain label is neither a lane nor a type; max 3 per issue.

### Status labels (situational)
Optional: `blocked`, `needs refinement`. Like domain labels, they are supplementary — not a lane or a type, and they do not satisfy the "1 Lane + 1 Type" requirement. Add during triage/grooming when they apply.

## 5. Priority policy
`Urgent` / `High` / `Medium` / `Low` / `No priority`
- the agent may **propose** priority
- set it automatically only for clear cases: security, data loss, hard blocker
- `Lane Now` and cycle are chosen by a human
- `Lane Ready` / `Lane Discovery` go through Triage review → priority gets corrected before the issue falls through the cracks

## 6. Forbidden things
- `triage:*` as a classification model instead of `Lane *`
- the old `ready` as a workflow label
- an issue without a lane / without a type
- multiple lanes or multiple types at once

## 7. Default behavior for triage
**Lane:** concrete → `Lane Ready` · unclear → `Lane Discovery` · valid but deferred → `Lane Later`
**Type:** bug → `Type Bug` · new build/delivery → `Type Feature` · arch/epic/research → `Type Discovery` · follow-up → `Type Follow-up` · refactor/cleanup → `Type Tech Debt` · routine upkeep/deps/config → `Type Chore`
**Routing:** `Lane Discovery` and `Lane Ready` → to Triage · `Lane Later` → straight to backlog · `Lane Now` → manually only

## 8. Agent-generated issues
An issue from Claude / an agent = AI-generated intake:
- `Lane Ready` and `Lane Discovery` are not finally approved just because an agent set them
- Triage is an explicit review checkpoint before entering the backlog (a second check of routing, type, and priority)

## 9. Hybrid model (practical step)
- templates = structured input
- agent = first classification
- triage = review checkpoint for `Lane Ready` and `Lane Discovery`
- backlog = only after acceptance in Triage, or straight away for `Lane Later` only
