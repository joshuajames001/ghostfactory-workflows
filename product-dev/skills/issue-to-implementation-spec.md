---
name: Issue to implementation spec
description: Converts an issue or request into an implementation spec with requirements, steps, and risks
scope: product-dev
---

Prepare an implementation spec from an issue or a brief request.

## Goal
Convert a product or technical request into a working plan for implementation.

## Input
An issue, feature request, bug report, or brief request.

## Procedure
1. Briefly summarize what should change and why.
2. Separate functional requirements from technical requirements.
3. Propose implementation steps in a logical order.
4. State dependencies on systems, data, integration points, or repositories.
5. Identify risks, edge cases, and missing information.
6. If it makes sense, propose a way to verify it or test scenarios.

## Output
Use this structure:
### Request summary
### Functional requirements
### Technical requirements
### Implementation steps
### Dependencies
### Risks and edge cases
### Validation / test scenarios
### Open questions

## Rules
- Write concisely and in technically understandable terms.
- Distinguish confirmed facts from proposals.
- When details are missing, prepare the best working proposal and explicitly list the gaps.
