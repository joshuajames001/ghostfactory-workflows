# Linear Skills

Reusable operační workflow moduly pro Claude (nebo jiného AI agenta) pracujícího v Linearu podle GF_AOS issue modelu.

Každý skill = jedna single-task instrukce. Všechny počítají s:
- `Lane Now / Ready / Discovery / Later`
- `Type Bug / Feature / Discovery / Follow-up / Tech Debt`
- zákazem `triage:*` a starého `ready`
- hybridním modelem: `Lane Ready` a `Lane Discovery` → Triage review, `Lane Later` → rovnou backlog

> Obecné (ne-Linear) skills — PRD rozpad, implementační spec, release notes, reporting — najdeš v [`../../product-dev/skills/`](../../product-dev/skills/).

---

## Skills

| Skill | Účel |
|---|---|
| [Create GF issues](create-gf-issues.md) | Vytváří nové issue rovnou podle policy, template rules a lane/type modelu |
| [Triage issue](triage-issue.md) | Rychlé triage rozhodnutí — 1× lane, 1× type, další krok, priorita |
| [Backlog grooming](backlog-grooming.md) | Ověří kvalitu a připravenost issue, odhalí missing info, rizika a závislosti |
| [Prioritizace backlog itemu](prioritize-backlog-item.md) | Konzervativní priorita podle dopadu, urgence a rizika |
| [Feature request do backlogu](feature-request-to-backlog.md) | Převede nápad do backlog issue, rozliší Feature vs Discovery |
| [Bug report z poznámek](bug-report-from-notes.md) | Převede neformální poznámky do kvalitního Bug issue |
| [Issue z neformálního zadání](issue-from-informal-input.md) | Převede kusé zadání do správně strukturovaného a zařazeného issue |

---

## Doporučené použití

**Session review** → `Create GF issues`, `Bug report z poznámek`, `Feature request do backlogu`, `Issue z neformálního zadání`

**Backlog hygiene** → `Triage issue`, `Backlog grooming`, `Prioritizace backlog itemu`

---

## Architektura workflow

- **Linear** = control plane: intake, triage, backlog, planning, execution handoff
- **Claude / agent** = operator: tvorba issue, prvotní klasifikace, převod poznámek do struktury
- **Člověk** = finální rozhodnutí: `Lane Now`, cycle selection, priority override, Triage review u `Lane Ready` a `Lane Discovery`

Nejdůležitější vrstva je tvorba a třídění issue:

- **Templates** dávají strukturu
- **Lane** říká, kdy a jak se má issue řešit
- **Type** říká, o jaký typ práce jde
- **Triage** je druhá kontrola pro issue s vyšším rozhodovacím rizikem

Model je přenositelný i do jiných AI-assisted týmů, kde issue často nevznikají ručně, ale přes agenty.
