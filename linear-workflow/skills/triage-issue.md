---
name: Triage issue
description: Assigns each issue a single Lane and Type, recommends the next step and a priority
scope: linear-workflow
---

When triaging an issue for GF_AOS, always treat the team docs as the source of truth:
- Final Issue Policy
- Automation Spec
- Short Agent Guidance
- Template Selection Rules

## Goal
Produce a quick, usable triage decision without breaking the GF_AOS workflow model.

## Mandatory model
Every issue must have:
- exactly 1 `Lane *`
- exactly 1 `Type *`
- optional domain labels
- a priority

Use only:
- `Lane Now`, `Lane Ready`, `Lane Discovery`, `Lane Later`
- `Type Bug`, `Type Feature`, `Type Discovery`, `Type Follow-up`, `Type Tech Debt`

Never use:
- `triage:*`
- the old `ready`
- multiple lane labels
- multiple type labels

## Procedure
1. Summarize the essence of the issue in one or two sentences.
2. Decide the correct `Type *`.
3. Decide the correct `Lane *`.
4. Propose the next step.
5. Assess whether the issue must go to Triage review or can go straight to the backlog.
6. Propose a conservative priority.
7. List the missing information.

## Type rules
- broken behavior / regression / wrong behavior → `Type Bug`
- new capability / delivery item → `Type Feature`
- research / epic / architectural decision / audit / open question → `Type Discovery`
- follows on from a review or an earlier issue → `Type Follow-up`
- refactor / cleanup / infra hardening / maintainability → `Type Tech Debt`
- if the issue contains open questions, an audit, or a decision before implementation, use `Type Discovery` even if it technically relates to cleanup or hardening

## Lane rules
- implementable, specific work → `Lane Ready`
- unclear scope / decision needed → `Lane Discovery`
- valid but not currently relevant work → `Lane Later`
- never set `Lane Now` automatically

## Triage routing
- `Lane Ready` → the issue should go to Triage review
- `Lane Discovery` → the issue should go to Triage review
- `Lane Later` → can go straight to the backlog

## Priority
- `Urgent` only for security, data loss, a hard blocker
- `High` for a clear release or delivery blocker
- otherwise be conservative: `Medium`, `Low`, `No priority`

## Output
Use this structure:
### Summary
### Type
### Lane
### Recommendation
### Triage routing
### Missing information
### Recommended priority

Write concisely, in decisive language, and do not invent details without flagging the uncertainty.
