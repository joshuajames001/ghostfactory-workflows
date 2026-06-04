# Claude Code Skill — `linear-workflow`

A bonus, **installable Claude Code skill** that bundles the entire Linear AI-first workflow into one instruction. Where the [agent personalization skills](../skills/) are individual single-task modules for your Linear agent, this is one meta-skill for **Claude Code** (or any agent that loads `SKILL.md` files) that knows the whole model: lane/type, Triage, routing, templates, priority, cycles.

## Synced with this repo

The skill is a thin layer over the repo's source of truth. Its **Sources of truth** section links directly to:
- [`../policy/`](../policy/) — Final Issue Policy, Automation Spec, Template Selection Rules
- [`../setup/`](../setup/) — the Linear agent guidance / automation config

Update those files and the skill stays in sync — it doesn't duplicate the rules, it points to them.

## Install

Copy the skill into your skills folder, naming the folder `linear-workflow`:

```bash
# user-level
cp SKILL.md ~/.claude/skills/linear-workflow/SKILL.md
# or project-level
cp SKILL.md <your-project>/.claude/skills/linear-workflow/SKILL.md
```

Then customize the placeholders (`<TEAM>`, `<PROJECT_*>`, `<DOMAIN_LABEL>`) — or point the Sources-of-truth links at your own copy of `policy/` and `setup/`.

The skill auto-triggers on phrases like "create an issue", "triage", "sprint planning", "issue from review" (see the `description` in `SKILL.md`).
