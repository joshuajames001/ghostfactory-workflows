---
name: Issue from informal input
description: Converts informal input into a correctly routed issue in the GF_AOS workflow model
scope: linear-workflow
---

When converting informal input into an issue for GF_AOS, always treat the team docs as the source of truth:
- Final Issue Policy
- Short Agent Guidance
- Template Selection Rules

## Goal
Convert informal input into a quality issue that is classified right away into the correct GF_AOS workflow model.

## Procedure
1. Decide whether it is a Bug, Feature, Discovery, Follow-up, or Tech Debt.
2. Pick the matching template.
3. Propose a short, specific title.
4. Write the issue in the structure matching the template.
5. Set exactly 1 `Lane *` and 1 `Type *`.
6. Propose a conservative priority.
7. List the missing information.

## Key rule
If the issue contains open questions, an audit, or a decision before implementation, use `Type Discovery` even if it technically relates to cleanup or hardening.

## Lane rules
- specific implementation → `Lane Ready`
- unclear / audit / decision → `Lane Discovery`
- valid but deferred → `Lane Later`
- never set `Lane Now` automatically

## Triage routing
- `Lane Ready` → to Triage review
- `Lane Discovery` → to Triage review
- `Lane Later` → can go straight to the backlog

## Output
Use the structure from the template, then add at the end:
### Lane
### Type
### Recommended priority
### Open questions

Do not invent hidden assumptions. If something is missing, state it explicitly.
