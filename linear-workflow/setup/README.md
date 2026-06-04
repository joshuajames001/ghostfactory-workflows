# Setup — kam co patří v Linearu

Tahle složka zrcadlí reálná nastavení v Linearu. Každý soubor = jedno pole, které vložíš do příslušné sekce.

| Soubor | Linear sekce |
|---|---|
| [`workspace-ai-agents/linear-agent-guidance.md`](workspace-ai-agents/linear-agent-guidance.md) | `settings/ai-agents` → workspace guidance (Linear agent) |
| [`workspace-ai-agents/agent-personalization.template.md`](workspace-ai-agents/agent-personalization.template.md) | `settings/ai-agents` → agent personalization (default guidance + skills) |
| [`team-workflow-triage/agent-automation.md`](team-workflow-triage/agent-automation.md) | `team-settings/workflow/triage` → agent automations |
| [`team-workflow-triage/triage-intelligence.template.md`](team-workflow-triage/triage-intelligence.template.md) | `team-settings/workflow/triage` → triage intelligence (extra guidance) |

Skills najdeš v [`../skills/`](../skills/), issue templates v [`../templates/`](../templates/), kanonickou policy v [`../policy/`](../policy/).

## Konvence placeholderů

- `<TEAM>` — název tvého týmu
- `<PROJECT>` — název projektu
- `<DOMAIN_LABEL>` — doménový label

Soubory s příponou `.template.md` obsahují placeholdery + blok `> Example (GhostFactory): …` s reálnou hodnotou jako ukázkou.
