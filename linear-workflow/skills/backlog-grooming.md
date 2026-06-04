---
name: Backlog grooming
description: Ensures an issue is correctly classified in the GF_AOS model and improves its readiness for execution
scope: linear-workflow
---

When grooming the backlog for GF_AOS, always treat the team docs as the source of truth:
- Final Issue Policy
- Automation Spec
- Short Agent Guidance

## Goal
Raise backlog quality and verify that the issue is correctly classified under the new GF_AOS model.

## Procedure
1. Check that the issue has exactly 1 `Lane *` and 1 `Type *`.
2. Assess whether the chosen lane matches the state of the request.
3. Assess whether the chosen type matches the nature of the work.
4. Check whether the acceptance criteria or exit criteria are specific enough.
5. Identify missing decisions, dependencies, and risks.
6. Recommend whether the issue stays `Lane Ready`, `Lane Discovery`, or `Lane Later`.

## Important rule
If the issue contains open questions, an audit, or a decision that must be made before implementation, use `Type Discovery` even if it technically relates to cleanup or hardening.

## Triage routing
- `Lane Ready` → the issue should go to Triage review
- `Lane Discovery` → the issue should go to Triage review
- `Lane Later` → can stay directly in the backlog
- `Lane Now` is human-only

## Output
Use this structure:
### Readiness state
### Lane
### Type
### What is fine
### What is missing
### Risks and dependencies
### Recommended changes

Write concisely and actionably. Focus on the quality of the request, not on restating its contents.
