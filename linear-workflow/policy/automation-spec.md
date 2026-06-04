# Automation Spec (template)

Jak se mají agent automations v týmu `<TEAM>` chovat při vytváření a úpravách issue.

## Cíl
Automations mají:
- udržovat konzistentní klasifikaci
- snižovat ruční backlog hygiene
- připravovat issue pro planning a execution
- nikdy nerozbíjet lane/type model
- posílat vyšší-rizikové AI-generated issues do Triage jako explicitní review checkpoint

Automations nemají: rozhodovat o aktivní práci místo člověka, vytvářet konfliktní klasifikaci, přepisovat správně zařazené issue bez důvodu.

## Povinný model
Každé issue: 1× `Lane *`, 1× `Type *`, 0–3 domain labels, priorita.
Zakázáno: `triage:*` jako hlavní model, starý `ready`.

## Automation 1 — On issue created by Claude / Linear Agent
**Smí:** doplnit `Lane *`, `Type *`, konzervativně navrhnout prioritu, doplnit domain label, rozhodnout o Triage review.
**Nesmí:** `Lane Now`, víc lane/type, `triage:*`, starý `ready`, přiřadit cycle, vytvářet follow-up.
**Lane:** konkrétní → `Lane Ready` · nejasné/epik/rozhodnutí → `Lane Discovery` · odložené → `Lane Later` · `Lane Now` jen ručně.
**Type:** dle Final Issue Policy; open questions/audit/rozhodnutí před implementací → `Type Discovery` i u cleanup/hardening.
**Priority:** `Urgent` jen security/data loss/hard blocker · `High` release/delivery blocker · jinak konzervativně.
**Routing:** `Lane Discovery` a `Lane Ready` → do Triage · `Lane Later` → rovnou backlog · `Lane Now` nikdy automaticky.

## Automation 2 — On issue updated
**Smí:** doplnit chybějící `Lane *`/`Type *`, odstranit zakázané labely, srovnat očividně nekonzistentní issue.
**Nesmí:** přepisovat správný lane/type bez důvodu, eskalovat na `Lane Now`, zvyšovat prioritu bez pravidla.
**Conflict resolution:** víc lane → ponechat konzervativnější (`Lane Discovery` > `Lane Later` > `Lane Ready`); víc type → ponechat nejlépe odpovídající. Při nejistotě `Lane Discovery`.

## Automation 3 — Legacy cleanup guard
Spustit při create / update / importu. Odstranit: `triage:now/ready/discovery/later`, starý `ready`. Ponechat: `Lane *`, `Type *`, domain labels.

## Domain labels
- **Common:** `Frontend`, `Backend`, `infra`, `Security`, `Testing`, `sdk`
- **Project-specific:** `<DOMAIN_LABEL>`

> Example (GhostFactory) — Span Chain: `ledger`, `otel`, `evals`, `runtime`, `observability`, `liveview`, `scale`, `versioning`

Omezení: max 3; domain label nenahrazuje type ani lane.

## Human-only decisions
`Lane Now` · cycle assignment · finální priority override · přijetí `Lane Ready`/`Lane Discovery` z Triage do backlogu · merge/zrušení issue.

## Expected output
Po vytvoření issue: 1× `Lane *`, 1× `Type *`, žádný legacy label, konzistentní priorita, případně domain labels, správné rozhodnutí o Triage review.
