# Linear for AI-First Issue Workflows

A practical tutorial for a solo-founder / AI-first product-development workflow on top of Linear, where issues are often created by Claude or another agent.

---

## The problem we're solving

A typical problem in an AI-assisted workflow:

- a session review takes place
- the review produces new issues
- in the next sprint those issues get worked on
- working on them produces yet more issues
- the backlog swells and you feel like you're running in place

Further complications:

- issues often aren't created manually in Linear, but via an external agent (e.g. Claude)
- if issues don't go through Triage, the team's Triage automations don't fire
- if there's no unified schema for labels / lane / type, agents quickly produce an inconsistent backlog

The goal is to make Linear a **control plane**, not just a place where tasks land.

---

## The core principle

Linear should be:

- the source of truth for planning
- the source of truth for triage
- the source of truth for backlog hygiene
- the source of truth for execution handoff

Agents are not the source of truth.
Agents should:

- help with structure
- help with classification
- help with creating issues
- but not determine active work without review

---

## Important finding: Triage is not a universal trigger

In Linear, Triage doesn't run periodically.
Triage works **event-driven** — when an issue **enters Triage**.

This means:

- an issue created by an integration or from outside the team may end up in Triage
- an issue created directly as a normal team issue into the backlog may not go through Triage at all

The practical consequence:

If Claude creates issues outside the Linear Agent chat and doesn't put them into Triage, then the following don't fire:

- Triage Intelligence
- Triage Rules
- Agent Automations tied to "when issue enters triage"

That's why you need a dual model:

1. **Claude-created issues** must be created correctly from the start
2. **Triage** serves as a review checkpoint for cases that actually enter it or that you deliberately send there

---

## Final issue schema for the GF_AOS team

Every issue should have:

- exactly **1 Lane**
- exactly **1 Type**
- optional domain labels
- a priority

### Lane labels

Use only:

- `Lane Now`
- `Lane Ready`
- `Lane Discovery`
- `Lane Later`

### Lane meaning

- `Lane Now`
  - actively being worked on right now
  - human manual decision only

- `Lane Ready`
  - concrete, implementable, ready for planning
  - for an AI-generated issue, should go through a review checkpoint

- `Lane Discovery`
  - a decision, validation, or scope breakdown is needed
  - should go through a review checkpoint

- `Lane Later`
  - valid work, but not now
  - can go straight to the backlog

### Type labels

Use only:

- `Type Bug`
- `Type Feature`
- `Type Discovery`
- `Type Follow-up`
- `Type Tech Debt`

### Type meaning

- `Type Bug`
  - broken behavior, regression, wrong behavior

- `Type Feature`
  - new capability or delivery item

- `Type Discovery`
  - research, epic, audit, architecture decision, open question

- `Type Follow-up`
  - follow-up work after a review or after a completed issue

- `Type Tech Debt`
  - refactor, cleanup, infra hardening, maintainability

### Forbidden labels

Do not use as a workflow model:

- `triage:*`
- the old `ready`

---

## A key rule that proved important

If an issue contains:

- open questions
- an audit
- a decision required before implementation

then it should be:

- `Type Discovery`

**even if it technically relates to cleanup or hardening**.

This is important because without this rule agents tend to cram "decision-first" issues into `Type Tech Debt`.

---

## Hybrid model for AI-generated issues

Not everything has to go through Triage, otherwise you create unnecessary overhead.

### Recommended model

- `Lane Discovery` → send to **Triage**
- `Lane Ready` → send to **Triage**
- `Lane Later` → may go straight to the **backlog**
- `Lane Now` → the agent never sets this

### Why this makes sense

`Lane Ready` and `Lane Discovery` are issues that affect near-term work or require a decision.
This is where you want an explicit checkpoint.

`Lane Later` are low-risk backlog items, where the review moment isn't as important.

---

## What this means for Claude-created issues

Because issues will often be created by external agents rather than by the Linear Agent in the Triage flow, Claude must be taught to:

- pick the right template
- write the issue in the right structure
- set the right lane
- set the right type
- be conservative with priority

You can't rely on "Triage fixing it later somewhere down the line".

---

## Templates are not a substitute for triage

Templates serve as **structured intake**.
That means they:

- raise the quality of the input
- improve the decision-making of both the agent and triage
- keep issue descriptions consistent

Templates by themselves don't decide:

- what is important
- what should be `Lane Ready`
- what is `Type Discovery`

But they help a lot with it.

---

## Recommended issue templates

### 1. Bug
Use when:

- something is broken
- it's a regression
- there is expected vs actual behavior

Structure:

```md
## What happened

## Why it matters

## Expected behavior

## Actual behavior

## Impact

## Acceptance criteria
- [ ]
- [ ]
- [ ]

## Related issue / review context
```

---

### 2. Feature
Use when:

- you're adding a new capability
- you're delivering a new screen, API, workflow, or delivery item

Structure:

```md
## Context

## Goal

## Scope
- 
- 
- 

## Out of scope
- 
- 

## Acceptance criteria
- [ ]
- [ ]
- [ ]
```

---

### 3. Discovery
Use when:

- implementation is not yet the goal
- a decision is missing
- it's about architecture, an audit, an epic, or an open question

Structure:

```md
## Context

## Problem / question

## Possible directions
- 
- 
- 

## Exit criteria
- [ ] we have a recommended decision
- [ ] we have the reason why
- [ ] we have a clear next step

## Source / references
```

---

### 4. Follow-up
Use when:

- the issue comes from a review
- it follows up on completed work
- you explicitly want to preserve continuity

Structure:

```md
## What

## Why

## Solution

## Acceptance criteria
- [ ]
- [ ]
- [ ]

## Context
```

---

### 5. Tech Debt
Use when:

- it's about cleanup, refactor, hardening, or maintainability
- it's not primarily about a new capability

Structure:

```md
## Problem

## Solution

## Done When
- [ ]
- [ ]
- [ ]

## Note
```

---

## Template selection rules

Use this simple mapping:

- broken behavior → **Bug**
- new capability → **Feature**
- not enough clarity / audit / need decision → **Discovery**
- came from previous issue or review → **Follow-up**
- cleanup / refactor / hardening without open decision → **Tech Debt**

---

## Priority rules

The agent should propose priority conservatively.

### Safe rule

- `Urgent`
  - security
  - data loss
  - hard blocker

- `High`
  - release blocker
  - significant delivery blocker

- otherwise:
  - `Medium`
  - `Low`
  - `No priority`

And it still holds that:

- the agent never sets `Lane Now`
- cycle selection is a human's manual decision

---

## What Triage is really good for in an AI workflow

Triage is useful as:

- an explicit review checkpoint
- the place where you fix a wrongly assigned lane/type/priority
- protection against a misclassified AI issue getting lost in the backlog

So for an AI-generated issue it mainly makes sense where:

- it's `Lane Ready`
- it's `Lane Discovery`

That's exactly the moment when you want a second check.

---

## What had to be cleaned up in practice

While rolling out the workflow, typical problems showed up:

- a dual lane model (`Lane *` vs `triage:*`)
- missing type labels
- the old `ready` label surviving in older projects
- agents creating issues outside Triage
- an unclear boundary between `Type Discovery` and `Type Tech Debt`

That's why it's important to first:

1. unify the labels
2. clean up representative projects
3. write the policy and guidance
4. create the templates
5. only then tune automations and MCP workflows

---

## Recommended rollout procedure

### Phase 1 — Team-level standard

Introduce for the whole team:

- `Lane *`
- `Type *`
- priority policy
- short guidance
- an automation spec

### Phase 2 — Clean up key projects

Clean up a few representative projects to create a reference model.

E.g.:

- Span Chain / Observability Core
- RAG GF AOS
- GhostFactory AOS 3.0

### Phase 3 — Templates

Introduce issue templates:

- Bug
- Feature
- Discovery
- Follow-up
- Tech Debt

### Phase 4 — Claude / agent skill

Create an agent skill that:

- loads the team docs
- picks the right template
- creates the issue already in the right shape

### Phase 5 — Validation in practice

First test on real session reviews.
Only then tune additional projects or more advanced MCP workflows.

---

## Recommended division of roles

### Linear
- planning
- triage
- backlog organization
- execution handoff
- source of truth

### Claude / external agent
- structured issue creation
- first classification
- priority proposal
- follow-up generation

### Human
- `Lane Now`
- cycle selection
- priority override
- review checkpoint in Triage

---

## Hard recommendation

If issues are mostly created by Claude:

- don't rely on Triage alone
- teach Claude to create issues correctly right from the start
- but also use Triage as a second check for `Lane Ready` and `Lane Discovery`

That's the most practical hybrid model.

---

## Summary in one sentence

The best AI-first workflow in Linear isn't "let the agent do everything", but building a system where:

- templates provide structure,
- the agent provides the first classification,
- triage provides the checkpoint,
- and the human decides on active work.
