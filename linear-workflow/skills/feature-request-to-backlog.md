---
name: Feature request to backlog
description: Convert an idea into a structured `<TEAM>` backlog issue with the right template and priority
scope: linear-workflow
---

When converting an idea into a backlog issue for `<TEAM>`, always treat the team docs as the source of truth:
- Final Issue Policy
- Short Agent Guidance
- Template Selection Rules

## Goal
Convert an idea into a structured issue suitable for backlog refinement and classify it correctly in the `<TEAM>` workflow.

## Procedure
1. Decide whether the `Feature` or `Discovery` template is more appropriate.
2. Write the issue using the structure of the matching template.
3. Separate the problem from the proposed solution.
4. Describe the benefit, scope, and open questions.
5. Set exactly 1 `Lane *` and 1 `Type *`.
6. Propose a conservative priority.

## Deciding
- new build / capability / delivery item → `Feature`
- unclear direction / question / audit / decision needed → `Discovery`
- if the scope boundaries are unclear, prefer `Discovery`

## Lane
- well-defined proposal → `Lane Ready`
- unclear proposal / validation needed → `Lane Discovery`
- valid but not currently relevant idea → `Lane Later`
- never set `Lane Now` automatically

## Type
- new capability → `Type Feature`
- open question / epic / audit → `Type Discovery`
- if the issue contains open questions before implementation, use `Type Discovery`

## Triage routing
- `Lane Ready` → to Triage review
- `Lane Discovery` → to Triage review
- `Lane Later` → can go straight to the backlog

## Output
Use this structure:
### Goal
### User / segment
### Problem
### Benefit
### Proposed scope
### Risks / dependencies
### Open questions
### Lane
### Type
### Recommended priority
