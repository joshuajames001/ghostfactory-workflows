<img src="assets/duo-mark.svg" alt="GhostFactory — ghost and robot" width="124" align="right">

# README_AI.md — Quick Reference for AI Agents

This file is the fast path. Read this first. Only go deeper if you need specifics.

---

## Quick Setup via MCP

Have Claude (or any MCP-connected agent) run this before creating any issues:

→ [`linear-workflow/setup/mcp-workspace-setup.md`](linear-workflow/setup/mcp-workspace-setup.md)

What it does: syncs the full label schema, creates the AI Agent Guidance
document in your team, and verifies Triage routing — in one pass.

Replace `<TEAM>` with your team name before running.

---

## The model

Every issue has exactly **1 Lane** and **1 Type**.

| Lane | When | Who sets it | Triage? |
|---|---|---|---|
| `Lane Now` | Active work | **Human only — never set automatically** | — |
| `Lane Ready` | Concrete, ready to implement | Agent | Yes |
| `Lane Discovery` | Unclear scope / decision needed | Agent | Yes |
| `Lane Later` | Valid but not now | Agent | No — straight to backlog |

| Type | When |
|---|---|
| `Type Bug` | Broken behavior, regression |
| `Type Feature` | New capability or deliverable |
| `Type Discovery` | Open question, audit, arch decision — **even if it looks like Tech Debt** |
| `Type Follow-up` | Comes from a review or completed issue |
| `Type Tech Debt` | Cleanup / refactor / hardening — **no open question** |
| `Type Chore` | Routine upkeep — deps / config / tooling / setup; **no user value, no code-quality change** |

**Triage routing:**
- `Lane Ready` and `Lane Discovery` → Triage checkpoint
- `Lane Later` → straight to backlog
- `Lane Now` → never set automatically

---

## Hard rules

- ❌ Never set `Lane Now`
- ❌ Never add an issue to a cycle without explicit instruction
- ❌ Never use `triage:*` or the old `ready` label
- ❌ Never leave an issue without a Lane or a Type
- ❌ Never overshoot priority — `Urgent` only for security / data loss / hard blocker
- ✅ When unsure between `Lane Ready` and `Lane Discovery` → use `Lane Discovery`
- ✅ When unsure between `Type Tech Debt` and `Type Discovery` (open question) → use `Type Discovery`

---

## Priority

| Priority | Use when |
|---|---|
| `Urgent` | Security, data loss, hard blocker |
| `High` | Release or delivery blocker |
| `Medium` / `Low` / `No priority` | Everything else — stay conservative |

---

## Where to find what

| Need | File |
|---|---|
| Full model + rollout guide | [`linear-workflow/workflow.md`](linear-workflow/workflow.md) |
| Canonical classification rules | [`linear-workflow/policy/final-issue-policy.md`](linear-workflow/policy/final-issue-policy.md) |
| Which template to pick | [`linear-workflow/policy/template-selection-rules.md`](linear-workflow/policy/template-selection-rules.md) |
| Label definitions + colors | [`linear-workflow/policy/label-schema.md`](linear-workflow/policy/label-schema.md) |
| Automation behavior rules | [`linear-workflow/policy/automation-spec.md`](linear-workflow/policy/automation-spec.md) |
| Issue templates | [`linear-workflow/templates/`](linear-workflow/templates/) |
| Linear agent skills | [`linear-workflow/skills/`](linear-workflow/skills/) |
| Linear settings setup | [`linear-workflow/setup/`](linear-workflow/setup/) |
| Claude Code skill | [`linear-workflow/claude-skill/SKILL.md`](linear-workflow/claude-skill/SKILL.md) |

---

## Template selection (quick)

- Broken behavior → `bug.md`
- New capability → `feature.md`
- Unclear / decision needed / audit → `discovery.md`
- Follows a review or completed issue → `follow-up.md`
- Cleanup / refactor / hardening, no open question → `tech-debt.md`
- Routine upkeep / deps / config / tooling, no user value → `chore.md`
