---
name: Issue z neformálního zadání
description: Převádí neformální zadání do správně směrovaného issue ve workflow GF_AOS modelu
scope: linear-workflow
---

Při převodu neformálního zadání do issue pro GF_AOS se vždy řiď team docs jako source of truth:
- Final Issue Policy
- Short Agent Guidance
- Template Selection Rules

## Cíl
Převést neformální zadání do kvalitního issue, které je rovnou zařazené do správného GF_AOS workflow modelu.

## Postup
1. Rozhodni, zda jde o Bug, Feature, Discovery, Follow-up nebo Tech Debt.
2. Vyber odpovídající template.
3. Navrhni krátký a konkrétní title.
4. Sepiš issue ve struktuře odpovídající template.
5. Nastav přesně 1 `Lane *` a 1 `Type *`.
6. Navrhni konzervativní prioritu.
7. Vypiš chybějící informace.

## Klíčové pravidlo
Pokud issue obsahuje otevřené otázky, audit nebo rozhodnutí před implementací, použij `Type Discovery`, i když technicky souvisí s cleanupem nebo hardeningem.

## Lane pravidla
- konkrétní implementace → `Lane Ready`
- nejasné / audit / rozhodnutí → `Lane Discovery`
- validní, ale odložené → `Lane Later`
- `Lane Now` nikdy automaticky

## Triage routing
- `Lane Ready` → do Triage review
- `Lane Discovery` → do Triage review
- `Lane Later` → může rovnou do backlogu

## Výstup
Použij strukturu podle template + přidej na konec:
### Lane
### Type
### Doporučená priorita
### Otevřené otázky

Nevymýšlej skryté předpoklady. Pokud něco chybí, napiš to explicitně.
