# Automation Spec (template)

How agent automations in the `<TEAM>` team should behave when creating and editing issues.

## Goal
Automations should:
- keep classification consistent
- reduce manual backlog hygiene
- prepare issues for planning and execution
- never break the lane/type model
- send higher-risk AI-generated issues to Triage as an explicit review checkpoint

Automations should not: decide on active work in place of a human, create conflicting classification, or rewrite correctly classified issues without reason.

## Mandatory model
Every issue: 1× `Lane *`, 1× `Type *`, 0–3 domain labels, priority.
Forbidden: `triage:*` as the main model, the old `ready`.

## Automation 1 — On issue created by Claude / Linear Agent
**May:** add `Lane *`, `Type *`, conservatively propose priority, add a domain label, decide on Triage review.
**Must not:** `Lane Now`, multiple lanes/types, `triage:*`, the old `ready`, assign a cycle, create follow-ups.
**Lane:** concrete → `Lane Ready` · unclear/epic/decision → `Lane Discovery` · deferred → `Lane Later` · `Lane Now` manually only.
**Type:** per the Final Issue Policy; open questions/audit/decision before implementation → `Type Discovery` even for cleanup/hardening.
**Priority:** `Urgent` only for security/data loss/hard blocker · `High` for release/delivery blocker · otherwise conservative.
**Routing:** `Lane Discovery` and `Lane Ready` → to Triage · `Lane Later` → straight to backlog · `Lane Now` never automatically.

## Automation 2 — On issue updated
**May:** add a missing `Lane *`/`Type *`, remove forbidden labels, align an obviously inconsistent issue.
**Must not:** rewrite a correct lane/type without reason, escalate to `Lane Now`, raise priority without a rule.
**Conflict resolution:** multiple lanes → keep the more conservative one (`Lane Discovery` > `Lane Later` > `Lane Ready`); multiple types → keep the best-fitting one. When in doubt, `Lane Discovery`.

## Automation 3 — Legacy cleanup guard
Run on create / update / import. Remove: `triage:now/ready/discovery/later`, the old `ready`. Keep: `Lane *`, `Type *`, domain labels.

## Domain labels
- **Common:** `Frontend`, `Backend`, `infra`, `Security`, `Testing`, `sdk`
- **Project-specific:** `<DOMAIN_LABEL>`

> Example (GhostFactory) — observability project: `ledger`, `otel`, `evals`, `runtime`, `observability`, `liveview`, `scale`, `versioning`

Constraints: max 3; a domain label does not replace a type or a lane.

## Status labels (situational)
Optional `blocked` / `needs refinement`. An automation may add or remove them when the situation clearly applies; they are supplementary and never substitute for a `Lane *` or `Type *`.

## Human-only decisions
`Lane Now` · cycle assignment · final priority override · accepting `Lane Ready`/`Lane Discovery` from Triage into the backlog · merging/closing an issue.

## Expected output
After an issue is created: 1× `Lane *`, 1× `Type *`, no legacy label, consistent priority, optionally domain labels, a correct decision about Triage review.
