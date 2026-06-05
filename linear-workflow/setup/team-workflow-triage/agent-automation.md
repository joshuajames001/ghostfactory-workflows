# Agent Automation — Triage

> Paste into `team-settings/workflow/triage` → agent automations.
> Generic text, no placeholders.

## Trigger
When any issue enters triage

## Then do only
- add exactly one Type label:
  - `Type Bug`
  - `Type Feature`
  - `Type Discovery`
  - `Type Follow-up`
  - `Type Tech Debt`
  - `Type Chore`
- add exactly one Lane label:
  - `Lane Later`
  - `Lane Discovery`
  - `Lane Ready`
- optionally add relevant domain labels

## Guardrails
- never set `Lane Now`
- never use `triage:*`
- never use old `ready`
- never add more than one lane
- never add more than one type
- do not move to cycle
- do not create follow-up issue automatically
