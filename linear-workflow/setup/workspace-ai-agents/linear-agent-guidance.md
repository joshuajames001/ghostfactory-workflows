# Linear Agent — Workspace Guidance

> Vlož do `settings/ai-agents` → workspace guidance (Linear agent).
> Text je generický, žádné placeholdery — funguje rovnou.

Use Linear as the control plane for all work.

## Core rules

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
- If scope is unclear or decision is needed → `Lane Discovery`
- If work is valid but not current → `Lane Later`

## Allowed Type labels
- `Type Bug`
- `Type Feature`
- `Type Discovery`
- `Type Follow-up`
- `Type Tech Debt`

### Type rules
- bug / regression / wrong behavior → `Type Bug`
- new capability / deliverable → `Type Feature`
- epic / research / architecture decision → `Type Discovery`
- work that follows previous issue or review → `Type Follow-up`
- refactor / cleanup / hardening / maintenance → `Type Tech Debt`
- if an issue contains open questions, audit work, or a decision that must happen before implementation, use `Type Discovery` even if it technically relates to cleanup or hardening

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
- `Lane Discovery` → send to Triage
- `Lane Ready` → send to Triage
- `Lane Later` → may go directly to backlog
- `Lane Now` → never automatic

## General behavior
- Prefer conservative classification
- If unsure, use `Lane Discovery`
- Never leave issue without lane or type
- Never apply multiple lane labels
- Never apply multiple type labels
- Do not create follow-up issues automatically unless explicitly requested
