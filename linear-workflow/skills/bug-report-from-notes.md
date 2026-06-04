---
name: Bug report z poznámek
description: Převede neformální bug poznámky do kvalitního issue v GF_AOS workflow
scope: linear-workflow
---

Při převodu poznámek do bug issue pro GF_AOS se vždy řiď team docs jako source of truth:
- Final Issue Policy
- Short Agent Guidance
- Template Selection Rules

## Cíl
Převést neformální bug poznámky do kvalitního issue ve správném GF_AOS workflow modelu.

## Vždy použij template `Bug`.

## Postup
1. Urči kontext vzniku problému.
2. Navrhni nebo doplň repro steps.
3. Odděl expected result a actual result.
4. Odhadni dopad.
5. Doplň acceptance criteria.
6. Nastav správný lane a type.
7. Navrhni konzervativní prioritu.

## Type
- vždy `Type Bug`, pokud jde o broken behavior nebo regression
- pokud po analýze zjistíš, že nejde o bug ale o audit / rozhodnutí, převeď to na `Type Discovery`

## Lane
- pokud je bug konkrétní a opravitelný → `Lane Ready`
- pokud chybí příčina nebo rozhodnutí před implementací → `Lane Discovery`
- pokud je validní, ale neaktuální → `Lane Later`
- `Lane Now` nikdy automaticky

## Triage routing
- `Lane Ready` → do Triage review
- `Lane Discovery` → do Triage review
- `Lane Later` → může rovnou do backlogu

## Výstup
Použij strukturu:
### What happened
### Why it matters
### Expected behavior
### Actual behavior
### Impact
### Acceptance criteria
### Related issue / review context
### Lane
### Type
### Doporučená priorita

Pokud repro steps nejsou jisté, označ je jako nepotvrzené. Piš stručně a věcně.
