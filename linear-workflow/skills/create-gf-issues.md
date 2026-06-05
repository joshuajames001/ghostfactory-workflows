---
name: Create GF issues
description: Create correctly labeled issues for GF_AOS with appropriate templates and conservative priority
scope: linear-workflow
---

When creating an issue for GF_AOS, always treat the team docs as the source of truth:
- Final Issue Policy
- Automation Spec
- Short Agent Guidance
- Template Selection Rules

Before creating an issue, first pick the correct issue template:
- Bug — broken behavior, regression, expected vs actual
- Feature — a new capability or delivery item
- Discovery — unclear scope, a question, an epic, an architectural decision
- Follow-up — work arising from a review or following on from a completed issue
- Tech Debt — refactor, cleanup, hardening, maintainability
- Chore — routine maintenance, dependency bumps, config, tooling, setup (no user value)

Create the issue correctly from the start; do not rely on Triage. Issues from Claude usually do not enter team Triage, so the lane and type must already be set at creation time.

Every issue must have:
- exactly 1 `Lane *` label
- exactly 1 `Type *` label
- optional domain labels
- a conservatively set priority

Use only these lane labels:
- `Lane Now`
- `Lane Ready`
- `Lane Discovery`
- `Lane Later`

Use only these type labels:
- `Type Bug`
- `Type Feature`
- `Type Discovery`
- `Type Follow-up`
- `Type Tech Debt`
- `Type Chore`

Never use:
- `triage:*`
- the old `ready`

Rules for the lane:
- never set `Lane Now` automatically
- if the issue is specific and implementable, use `Lane Ready`
- if the issue contains open questions or needs an audit or a decision before implementation, use `Lane Discovery`
- if the work is valid but not currently relevant or deferred, use `Lane Later`

Rules for the type:
- broken behavior / regression / wrong behavior → `Type Bug`
- new capability / new screen / API / workflow / delivery → `Type Feature`
- research / epic / architectural decision / open question → `Type Discovery`
- follows on from a review, retrospective, or previous issue → `Type Follow-up`
- refactor / cleanup / infra hardening / maintainability → `Type Tech Debt`
- routine maintenance / dependency bumps / config / tooling / setup with no user value and no code-quality change → `Type Chore`
- if the issue contains open questions, an audit, or a decision that must be made before implementation, use `Type Discovery` even if it technically relates to cleanup or hardening

Priority:
- `Urgent` only for security, data loss, or a hard blocker
- `High` for a clear release or delivery blocker
- otherwise be conservative: `Medium`, `Low`, or `No priority`
- do not overshoot the priority

When writing the issue, use the structure matching the chosen template.

For a Bug, use the sections:
- What happened
- Why it matters
- Expected behavior
- Actual behavior
- Impact
- Acceptance criteria
- Related issue / review context

For a Feature, use the sections:
- Context
- Goal
- Scope
- Out of scope
- Acceptance criteria

For a Discovery, use the sections:
- Context
- Problem / question
- Possible directions
- Exit criteria
- Source / reference

For a Follow-up, use the sections:
- What
- Why
- Solution
- Acceptance criteria
- Context

For a Tech Debt, use the sections:
- Problem
- Solution
- Done When
- Note

For a Chore, use the sections:
- Task
- Done When
- Note

During session review:
- for each point, first decide whether it is a Bug, Feature, Discovery, Follow-up, Tech Debt, or Chore
- create an issue only when it is genuinely standalone work
- if you are unsure between `Lane Ready` and `Lane Discovery`, choose `Lane Discovery`
- if you are unsure between `Type Feature` and `Type Tech Debt`, consider whether it is a new capability or just an implementation improvement
- if you are unsure between `Type Tech Debt` and `Type Discovery`, and the issue contains open questions, an audit, or a decision before implementation, choose `Type Discovery`

The goal is for new issues to be created in the correct shape right away, with no need for a follow-up triage fix.
