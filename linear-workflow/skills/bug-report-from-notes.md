---
name: Bug report from notes
description: Converts informal bug notes into a quality issue in the `<TEAM>` workflow
scope: linear-workflow
---

When converting notes into a bug issue for `<TEAM>`, always treat the team docs as the source of truth:
- Final Issue Policy
- Short Agent Guidance
- Template Selection Rules

## Goal
Convert informal bug notes into a quality issue in the correct `<TEAM>` workflow model.

## Always use the `Bug` template.

## Procedure
1. Determine the context in which the problem arose.
2. Propose or fill in repro steps.
3. Separate the expected result from the actual result.
4. Estimate the impact.
5. Add acceptance criteria.
6. Set the correct lane and type.
7. Propose a conservative priority.

## Type
- always `Type Bug` if it concerns broken behavior or a regression
- if your analysis shows that it is not a bug but an audit / decision, convert it to `Type Discovery`

## Lane
- if the bug is specific and fixable → `Lane Ready`
- if the cause is unknown or a decision is needed before implementation → `Lane Discovery`
- if it is valid but not currently relevant → `Lane Later`
- never set `Lane Now` automatically

## Triage routing
- `Lane Ready` → to Triage review
- `Lane Discovery` → to Triage review
- `Lane Later` → can go straight to the backlog

## Output
Use this structure:
### What happened
### Why it matters
### Expected behavior
### Actual behavior
### Impact
### Acceptance criteria
### Related issue / review context
### Lane
### Type
### Recommended priority

If the repro steps are uncertain, mark them as unconfirmed. Write concisely and factually.
