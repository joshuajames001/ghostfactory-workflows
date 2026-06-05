# Template Selection Rules (template)

Rules for choosing an issue template in the `<TEAM>` team. A template does not guarantee final triage, but it significantly improves decision quality. See [`../templates/`](../templates/).

## 1. Bug
Use when: something is broken, a regression, the system behaves differently than it should, there is an expected vs actual.
Maps to: `Type Bug` · `Lane Ready` (clear what to fix) or `Lane Discovery` (the cause must be found first) → to Triage.

## 2. Feature
Use when: you are adding a new capability / screen / API / workflow / product value and the scope is aimed at implementation.
Maps to: `Type Feature` · `Lane Ready` (→ Triage review) or `Lane Later` (valid, but not now).

## 3. Discovery
Use when: implementation is not yet the goal, a decision is missing, you are working through architecture/options/unclear scope, or it's an epic, an audit, or a research question.
Maps to: `Type Discovery` · `Lane Discovery` → to Triage.

## 4. Follow-up
Use when: the issue follows up on a review or previously completed work, it's a next step outside the original scope, or you want to preserve continuity.
Maps to: `Type Follow-up` · `Lane Later` or `Lane Ready` (→ Triage).

## 5. Tech Debt
Use when: it's not primarily about a new capability, and the goal is cleanup / refactor / maintainability / infra hardening.
Maps to: `Type Tech Debt` · `Lane Ready` (concrete) or `Lane Later`.
Caution: if the issue contains open questions before implementation → it's not Tech Debt, but Discovery.

## 6. Chore
Use when: routine maintenance, dependency bumps, configuration, tooling/CI, or setup/ops work with no direct user value and no code-quality change.
Maps to: `Type Chore` · `Lane Later` (usually) or `Lane Ready` (if needed soon).
Boundary: improves existing code quality → Tech Debt; pure upkeep with no user value → Chore; open question first → Discovery.

## Quick decision rule
- broken behavior → **Bug**
- new capability → **Feature**
- not enough clarity / need decision / audit before action → **Discovery**
- came from previous issue/review → **Follow-up**
- cleanup / refactor / hardening without open decision → **Tech Debt**
- routine upkeep / deps / config / CI without code-quality change → **Chore**

## Priority & Triage reminder
- `Lane Now` never automatically; priority conservatively; active work and cycle are chosen by a human
- AI-generated: `Lane Discovery` and `Lane Ready` → to Triage · `Lane Later` → straight to backlog
