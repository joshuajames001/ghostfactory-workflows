---
name: Prioritize backlog item
description: Recommends a conservative priority for a GF_AOS backlog item based on impact, urgency, and the lane/type rules
scope: linear-workflow
---

When prioritizing a backlog item for GF_AOS, always treat the team docs as the source of truth:
- Final Issue Policy
- Automation Spec
- Short Agent Guidance

## Goal
Give a quick, usable priority recommendation without false certainty and without breaking the lane/type model.

## Procedure
1. Evaluate the impact on the user or the system.
2. Assess urgency and time sensitivity.
3. Consider the risk of deferring.
4. Verify that the item matches its lane and type.
5. Propose a conservative priority.
6. If data is missing, prepare options based on assumptions.

## Priority rules
- `Urgent` only for security, data loss, or a hard blocker
- `High` for a clear release or delivery blocker
- otherwise be conservative: `Medium`, `Low`, `No priority`

## Lane reminder
- `Lane Now` is human-only
- `Lane Ready` and `Lane Discovery` should go to Triage review
- `Lane Later` can go straight to the backlog

## Output
Use this structure:
### Impact
### Urgency
### Risk
### Recommended priority
### Note on lane/type
### Options

Do not state firm conclusions where the supporting information is missing. If the classification is unclear, say so explicitly.
