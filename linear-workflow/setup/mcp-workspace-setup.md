# Setup GhostFactory Linear Workspace via MCP

## Context

This prompt provisions a Linear workspace for the AI-first workflow defined in
[ghostfactory-workflows](https://github.com/joshuajames001/ghostfactory-workflows).

**Replace before running:**
- `<TEAM>` — team name or ID (e.g. `GF_AOS`, `Span Chain`)

**What MCP handles automatically:**
- ✅ Label schema (Lane + Type + Domain + Status)
- ✅ AI Agent Guidance document
- ✅ Triage routing verification

**What requires manual UI setup (printed at the end):**
- Team Settings → Workflow → Triage → Toggle ON
- Issue templates
- Triage Intelligence / Linear Agent instructions

---

## What exists

Step 0: Read the current workspace state **before** writing anything:

```
list_issue_labels(team: "<TEAM>", limit: 250)
list_documents(team: "<TEAM>")
```

Store the results in memory — you will use them in Task 1 and Task 2 for skip-if-exists logic.

---

## Task

### 1. Synchronise label schema

For each label in the tables below:
- Check whether a label with the same `name` exists in the Step 0 results
- If it **exists** → skip it, log `⏭️ skipped: <name>`
- If it **does not exist** → create it with `create_issue_label`, log `✅ created: <name>`
- **Never modify an existing label**

Process labels sequentially (one at a time), not in parallel.

---

**Lane labels** — required on every issue

| name | color | description |
|---|---|---|
| Lane Now | #DC2626 | Actively being worked on right now |
| Lane Ready | #2563EB | Fully specified and next in queue |
| Lane Discovery | #7C3AED | Needs a decision, validation, or refinement before work can start |
| Lane Later | #6B7280 | Valid work, but not now |

---

**Type labels** — required on every issue

| name | color | description |
|---|---|---|
| Type Bug | #DC2626 | Bug or regression behaviour |
| Type Feature | #2563EB | New capability or user-facing value |
| Type Tech Debt | #6B7280 | Refactor, cleanup, maintainability or hardening |
| Type Discovery | #7C3AED | Goal is a decision, validation, or refinement |
| Type Follow-up | #D97706 | Follows from a previous issue, review, or completed work |
| Type Chore | #9CA3AF | Maintenance, setup, configuration — no direct user value |

---

**Domain labels** — apply when relevant

| name | color | description |
|---|---|---|
| Frontend | #10B981 | UI, components, styling |
| Backend | #0EA5E9 | API, server, database logic |
| infra | #6B7280 | Infrastructure, DevOps, deployment, environment |
| Security | #EF4444 | Auth, RLS, rate limiting, GDPR |
| Testing | #10B981 | Test coverage, test infrastructure, QA |
| sdk | #0EA5E9 | SDK development, client libraries, integrations |

---

**Status labels** — situational

| name | color | description |
|---|---|---|
| blocked | #EF4444 | Blocked by a decision, dependency, or missing input |
| needs refinement | #F59E0B | Right direction, but not enough detail to start work |

---

### 2. Create AI Agent Guidance document

Check whether a document named `"AI Agent Guidance"` already exists in the Step 0 results:
- If it **exists** → skip it, log `⏭️ skipped: AI Agent Guidance document`
- If it **does not exist** → create it:

```
save_document(
  team: "<TEAM>",
  title: "AI Agent Guidance",
  content: <content below>
)
```

**Document content (insert verbatim):**

```markdown
# AI Agent Guidance

> Source of truth for AI agents creating issues in this workspace.
> Human-readable version: ghostfactory-workflows/linear-workflow/workflow.md

---

## Required fields on every issue

| Field | Rule |
|---|---|
| Title | Imperative verb + concrete subject. Max 80 chars. |
| State | Always `Triage` — never set directly to Backlog or active states. |
| Lane label | Exactly one: Lane Now / Lane Ready / Lane Discovery / Lane Later |
| Type label | Exactly one: Type Bug / Type Feature / Type Tech Debt / Type Discovery / Type Follow-up / Type Chore |
| Priority | Propose conservatively. See rules below. |
| Description | Use the correct template. See Template Selection below. |

---

## Priority rules

| Level | Use when |
|---|---|
| Urgent | Security vulnerability, data loss, or hard blocker on active work |
| High | Release blocker or significant delivery blocker |
| Medium | Degrades quality or slows delivery, but not blocking |
| Low | Nice-to-have, cleanup, minor UX |
| No priority | Default — use when unsure |

> ⚠️ Never auto-escalate to Urgent or High unless the criteria above are met.
> Propose priority; a human confirms during Triage review.

---

## Lane rules

| Lane | Use when |
|---|---|
| Lane Now | Issue is actively being worked on this moment |
| Lane Ready | Fully specified, next in queue — do NOT assign during Triage |
| Lane Discovery | Needs a decision, validation, or refinement before work can start |
| Lane Later | Valid but not now — default for new issues from session review |

> Default for new issues: **Lane Later** unless there is an explicit reason for Lane Discovery or Lane Ready.
> **Lane Now** is set by a human only — never by an agent.

---

## Template selection

| Situation | Template |
|---|---|
| Something is broken | Type Bug → bug template |
| New capability or user value | Type Feature → feature template |
| Needs research or a decision | Type Discovery → discovery template |
| Follows from previous work | Type Follow-up → follow-up template |
| Cleanup, refactor, hardening (code quality) | Type Tech Debt → tech-debt template |
| Routine maintenance, deps, config, setup (no user value) | Type Chore → chore template |

Templates: `ghostfactory-workflows/linear-workflow/templates/`

---

## Routing to Triage

Always set `state: "Triage"` explicitly in `save_issue`.
Do not rely on "no project assigned" — it has no effect on Triage routing.

| Method | Notes |
|---|---|
| `state: "Triage"` in save_issue | Explicit — always works. Use this. |
| Create from within the Triage view | Manual UI only |
| Created via integration (MCP, Slack, Sentry) | Automatic — but be explicit anyway |

---

## What agents must NOT do

- ❌ Set Lane Now — human decision only
- ❌ Set state to anything other than Triage on new issues
- ❌ Auto-escalate priority to Urgent or High without meeting the criteria above
- ❌ Create issues without both a Lane and a Type label
- ❌ Create duplicate issues — search before creating
```

---

### 3. Verify Triage routing

Create a test issue:

```
save_issue(
  team: "<TEAM>",
  title: "[MCP Setup] Triage routing verification — delete after",
  state: "Triage",
  description: "Auto-generated by workspace setup. Cancel after confirming statusType = triage."
)
```

Check the response:
- `statusType === "triage"` → ✅ Triage routing works
- anything else → ⚠️ Log a warning — check that Triage is enabled in Team Settings

Then immediately cancel the test issue:

```
save_issue(id: "<test-issue-id>", state: "Canceled")
```

---

## Constraints

- Never modify existing labels — only create missing ones
- Never modify existing documents — only create "AI Agent Guidance" if absent
- Do not create any issues outside of Task 3 (the test)
- If a label or document already exists: skip silently, do not log an error
- Process labels **sequentially** — not in parallel; Linear has rate limits

---

## Done When

- `list_issue_labels(team: "<TEAM>")` returns all Lane + Type + Domain + Status labels
- Document "AI Agent Guidance" exists in the team
- Triage test ran and was cancelled (`statusType: "canceled"`)
- Setup Report printed in this format:

```
## Setup Report — GhostFactory Linear Workspace

### Labels
✅ created: Lane Now
⏭️ skipped: Lane Ready (already existed)
... (one line per label)

Created: X / Skipped: Y / Total: Z

### Documents
✅ created: AI Agent Guidance
(or ⏭️ skipped)

### Triage routing
✅ confirmed (statusType: triage)

---

## Manual steps required (UI only)

1. Team Settings → Workflow → Triage → Toggle ON
   (skip if already enabled)

2. Issue Templates → add templates from:
   ghostfactory-workflows/linear-workflow/templates/
   (bug.md, feature.md, discovery.md, follow-up.md, tech-debt.md, chore.md)

3. Team Settings → Triage → Linear Agent Instructions → paste content from:
   ghostfactory-workflows/linear-workflow/setup/workspace-ai-agents/linear-agent-guidance.md

4. Verify: open Triage view (G then T) — should appear in the sidebar
```
