# Setup — where everything goes in Linear

This folder mirrors the actual settings in Linear. Each file = one field that you paste into the corresponding section.

| File | Linear section |
|---|---|
| [`workspace-ai-agents/linear-agent-guidance.md`](workspace-ai-agents/linear-agent-guidance.md) | `settings/ai-agents` → workspace guidance (Linear agent) |
| [`workspace-ai-agents/agent-personalization.template.md`](workspace-ai-agents/agent-personalization.template.md) | `settings/ai-agents` → agent personalization (default guidance + skills) |
| [`team-workflow-triage/agent-automation.md`](team-workflow-triage/agent-automation.md) | `team-settings/workflow/triage` → agent automations |
| [`team-workflow-triage/triage-intelligence.template.md`](team-workflow-triage/triage-intelligence.template.md) | `team-settings/workflow/triage` → triage intelligence (extra guidance) |

Run once via MCP (not a paste-into-settings file):

- `mcp-workspace-setup.md` — one-shot MCP prompt: label schema + AI Agent Guidance doc + Triage verification

Skills in [`../skills/`](../skills/) are registered in the **Skills** section of `agent personalization` (below guidance). Issue templates are in [`../templates/`](../templates/) and the canonical policy in [`../policy/`](../policy/).

## Placeholder conventions

- `<TEAM>` — the name of your team
- `<PROJECT>` — the name of the project
- `<DOMAIN_LABEL>` — a domain label

Files with the `.template.md` suffix contain placeholders + a `> Example (GhostFactory): …` block with a real value as an illustration.
