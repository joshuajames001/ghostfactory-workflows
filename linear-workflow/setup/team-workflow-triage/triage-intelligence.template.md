# Triage Intelligence — Extra Guidance (template)

> Paste into `team-settings/workflow/triage` → triage intelligence (extra guidance).
> The model is generic; adjust only the **Routing hints** section (projects + domain labels) to your own.

This workspace contains multiple products and agent-assisted workflows. Use Linear as the control plane for planning, triage, execution handoff, and backlog hygiene.

Every issue must have:
- exactly 1 `Lane *` label
- exactly 1 `Type *` label
- optional domain labels
- a priority

## Allowed Lane labels
- `Lane Now`
- `Lane Ready`
- `Lane Discovery`
- `Lane Later`

### Lane rules
- Never set `Lane Now` automatically
- If scope is clear and implementation-ready → `Lane Ready`
- If scope is unclear or a decision is needed before implementation → `Lane Discovery`
- If work is valid but not current → `Lane Later`

## Allowed Type labels
- `Type Bug`
- `Type Feature`
- `Type Discovery`
- `Type Follow-up`
- `Type Tech Debt`

### Type rules
- broken behavior / regression / wrong behavior → `Type Bug`
- new capability / delivery item → `Type Feature`
- research / epic / architecture decision / audit / open question → `Type Discovery`
- work that follows a previous issue or review → `Type Follow-up`
- refactor / cleanup / hardening / maintenance → `Type Tech Debt`
- If an issue contains open questions, audit work, or a decision that must happen before implementation, use `Type Discovery` even if it technically relates to cleanup or hardening.

## Forbidden labels
Do not use:
- `triage:*`
- old `ready`

## Priority behavior
- Agents may propose priority
- Only auto-escalate for: security, data loss, hard blocker
- Otherwise stay conservative

## Human-only decisions
Only humans decide:
- `Lane Now`
- cycle assignment
- ambiguous priority overrides
- accepting `Lane Ready` and `Lane Discovery` issues from Triage into backlog

## Triage routing
For AI-generated issues:
- `Lane Discovery` → keep in / send to Triage for review
- `Lane Ready` → keep in / send to Triage for review
- `Lane Later` → may go directly to backlog
- `Lane Now` → never automatic

## Routing hints
Use project and domain context conservatively. Map by keyword → `<PROJECT>`:

- `<DOMAIN_LABEL>`, … → `<PROJECT_A>`
- `<DOMAIN_LABEL>`, … → `<PROJECT_B>`
- `<DOMAIN_LABEL>`, … → `<PROJECT_C>`

> Example (GhostFactory):
> - replay, evals, traces, ledger, OTLP, observability, liveview → Observability Core
> - RAG, embeddings, retrieval, reranking, GitHub + Linear context → RAG GF AOS
> - agent orchestration, control plane, execution plane, HITL, Ghost Channel → GhostFactory AOS 3.0

If routing is unclear, do not force a project aggressively. Prefer conservative classification and leave the project unchanged unless there is strong evidence.

## General behavior
- Prefer conservative classification
- If unsure, use `Lane Discovery`
- Never leave issue without lane or type
- Never apply multiple lane labels
- Never apply multiple type labels
- Do not create follow-up issues automatically unless explicitly requested
