---
name: linear-workflow
description: >
  Single source of truth for working with a Linear workspace — how to write, classify and plan issues.

  Use WHENEVER you hear: "create an issue", "write an issue", "add to Linear",
  "what goes into the cycle", "review an issue", "sprint planning", "triage", "how to write an issue",
  "prepare the backlog", "what goes into the sprint", "Linear issue", "issue from review".
---

# Linear Workflow

A portable Claude Code skill that bundles the full Linear AI-first workflow into one instruction. It stays in sync with this repo: the rules below mirror — and link to — the canonical [`policy/`](../policy/) and [`setup/`](../setup/) files. Update those, and the skill follows.

## Workspace setup (SSoT)

| Setting | Value |
|---------|-------|
| Team | `<TEAM>` |
| Cycles | 1 week, starting Monday |
| Triage | ON — for externally created issues |
| Triage Intelligence | ON — suggests project, label, assignee |
| Agent automations | ON — lane + type classification |
| PR flow | PR open → In Progress → In Review → Done |

> Example values — adjust to your workspace.

---

## Sources of truth (read before creating an issue)

When creating an issue, always follow:
- **[Final Issue Policy](../policy/final-issue-policy.md)**
- **[Automation Spec](../policy/automation-spec.md)**
- **[Short Agent Guidance](../setup/workspace-ai-agents/linear-agent-guidance.md)**
- **[Template Selection Rules](../policy/template-selection-rules.md)**

---

## Key rule

Every issue must have:
- exactly **1 `Lane *` label**
- exactly **1 `Type *` label**
- optional domain labels
- a priority set **conservatively**

### Triage as a double-check

Issues from Claude pass through Triage as a **checkpoint before the backlog**:

| Lane Claude sets | Behavior |
|------------------|----------|
| `Lane Discovery` | → Triage (unclear scope = always review) |
| `Lane Ready` | → Triage (verify AC before entering the backlog) |
| `Lane Later` | → straight to backlog (low urgency, low risk) |
| `Lane Now` | Claude never sets it |

The goal is to catch Type / Lane / Priority / Routing mistakes **in one place** (the Triage inbox), not scattered across the backlog.

---

## Products (routing)

| Keywords | Project |
|----------|---------|
| `<DOMAIN_LABEL>`, … | `<PROJECT_A>` |
| `<DOMAIN_LABEL>`, … | `<PROJECT_B>` |
| `<DOMAIN_LABEL>`, … | `<PROJECT_C>` |

> Example (GhostFactory):
> - observability backend, replay, evals, ledger, OTLP, trail UI, session tracing → Observability Core
> - orchestration shell, multi-agent runtime, product shell, agent platform → GhostFactory AOS

**Routing rules:**
- Map by keyword conservatively.
- If routing is unclear → classify conservatively and leave the decision to a human.

---

## Lane labels

Use **only these** — no others:

| Label | When |
|-------|------|
| `Lane Now` | Current work — **NEVER set automatically** |
| `Lane Ready` | Concrete and implementable, AC defined |
| `Lane Discovery` | Open questions, needs an audit or a decision before implementation |
| `Lane Later` | Valid work, but not current or deferred — **DEFAULT** |

**Lane rules:**
- Never set `Lane Now` automatically
- When in doubt, `Lane Discovery` — not `Lane Ready`
- Never use: `triage:*`, the old `ready`

---

## Type labels

Use **only these** — no others:

| Label | When |
|-------|------|
| `Type Bug` | Broken behavior, regression, wrong behavior |
| `Type Feature` | New capability, screen, API, workflow, delivery item |
| `Type Discovery` | Research, epic, architecture decision, open question |
| `Type Follow-up` | Follows up on a review, retro, or a previous issue |
| `Type Tech Debt` | Refactor, cleanup, infra hardening, maintainability |

**Type rules:**
- If an issue contains open questions, an audit, or a decision required before implementation → `Type Discovery`, even if it technically relates to cleanup or hardening
- Unsure between `Type Feature` and `Type Tech Debt` → ask whether it's a new capability or just an implementation improvement
- Unsure between `Type Tech Debt` and `Type Discovery` with open questions → `Type Discovery`

---

## Priority rules

| Priority | Criterion |
|----------|-----------|
| **Urgent** | Security, data loss, hard blocker |
| **High** | Clear release or delivery blocker |
| **Medium** | UX improvement, refactor, regular feature |
| **Low / No priority** | Nice-to-have, vague idea |

> Don't overshoot priority. Stay conservative.

---

## Issue templates

### Bug
```
## What happened
[what's happening]

## Why it matters
[impact on user or system]

## Expected behavior
[what should have happened]

## Actual behavior
[what happened]

## Impact
[scope, who and what is affected]

## Acceptance criteria
- [ ] ...

## Related issue / review context
[link or context]
```

### Feature
```
## Context
[why this feature exists]

## Goal
[what the feature should enable]

## Scope
[what's included]

## Out of scope
[what is deliberately not included]

## Acceptance criteria
- [ ] ...
```

### Discovery
```
## Context
[background and situation]

## Problem / question
[what we need to find out or decide]

## Possible directions
[known options or hypotheses]

## Exit criteria
[how we know the discovery is done]

## Source / reference
[ADR, doc, issue, discussion]
```

### Follow-up
```
## What
[what needs to be done]

## Why
[why it came up]

## Solution
[proposed approach]

## Acceptance criteria
- [ ] ...

## Context
[link to the original issue or review]
```

### Tech Debt
```
## Problem
[what's wrong and why]

## Solution
[proposed approach]

## Done When
[concrete completion condition]

## Note
[risks, dependencies, context]
```

---

## Issue anatomy (summary)

```
Title:       [verb + object], max 60 chars
             ✅ "Fix invoice PDF encoding for special chars"
             ❌ "PDF problem" / "Fix things in PDF"

Lane label:  Lane Now | Lane Ready | Lane Discovery | Lane Later
Type label:  Type Bug | Type Feature | Type Discovery | Type Follow-up | Type Tech Debt
Priority:    conservative — Urgent only for security/data loss/hard blocker
Description: use the template matching the chosen Type
```

---

## What the agent does when creating an issue

1. Picks the right **template** for the situation (Bug / Feature / Discovery / Follow-up / Tech Debt)
2. Proposes a **title** (max 60 chars, verb + object)
3. Fills the **description** per the template structure
4. Sets exactly **1 Type label** + exactly **1 Lane label**
5. Sets **priority conservatively**
6. **Never** sets `Lane Now`
7. **Never** adds an issue to a cycle without an explicit instruction
8. If the issue has enough information → creates it directly, no questions
9. If there isn't enough information → sets `Lane Discovery`, doesn't block with dialog

---

## Session review rules

- For each review point, decide: Bug / Feature / Discovery / Follow-up / Tech Debt
- Create an issue only for **genuinely separate work**
- Unsure `Lane Ready` vs `Lane Discovery` → choose **`Lane Discovery`**
- Unsure `Type Feature` vs `Type Tech Debt` → weigh new capability vs implementation improvement
- Unsure `Type Tech Debt` vs `Type Discovery` with open questions → **`Type Discovery`**
- Max **3 new issues** per review session; the rest → `Lane Later` or Cancelled

---

## Cycle rules

- Max **6–8 issues** per cycle
- Default: `Lane Ready` + `Urgent` or `High`
- Exception for `Medium`: closes a milestone / removes a blocker tail / needed for continuity
- Unfinished issues → rollover by a human's decision

---

## Red flags

- ❌ Setting `Lane Now` automatically
- ❌ Adding an issue to a cycle without confirmation
- ❌ Using `triage:*` or the old `ready` label
- ❌ Creating an issue without a Lane or Type label
- ❌ Overshooting priority (Urgent for a non-blocker)
- ❌ Mixing Bug + Feature + Discovery into one issue
- ❌ Blocking with dialog questions when it can be conservatively filed as `Lane Discovery`
- ❌ Relying on Triage to fix a badly-set issue
