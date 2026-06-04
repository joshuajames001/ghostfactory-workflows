---
name: PRD or note to issue tree
description: Converts a PRD or notes into an issue tree with workstreams and dependencies for execution planning
scope: product-dev
---

Break a PRD, notes, or a larger request down into a set of related issues.

## Goal
Convert a larger request into a practical issue tree suitable for planning and execution.

## Input
A PRD, a technical note, meeting notes, or a larger product request.

## Procedure
1. Briefly summarize the main goal and expected outcome.
2. Split the work into logical workstreams or thematic blocks.
3. For each block, propose standalone issues.
4. For each issue, write a short title and 1–3 sentences of description.
5. Mark dependencies, ordering, and what can run in parallel.
6. If something is not clear enough, note it as an open point.

## Output
Use this structure:
### Goal summary
### Proposed workstreams
### Issue tree
- parent / main block
- follow-on issues
- dependencies

### Open questions
### Recommended execution order

## Rules
- Prefer smaller, actionable issues over overly broad blocks.
- Distinguish between discovery, implementation, and follow-up work.
- If the scope is too large, propose an MVP variant and subsequent phases.
