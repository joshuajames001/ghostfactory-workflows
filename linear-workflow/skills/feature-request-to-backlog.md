---
name: Feature request do backlogu
description: Převeď nápad do strukturovaného GF_AOS backlog issue s vhodným šablonováním a prioritou
scope: linear-workflow
---

Při převodu nápadu do backlog issue pro GF_AOS se vždy řiď team docs jako source of truth:
- Final Issue Policy
- Short Agent Guidance
- Template Selection Rules

## Cíl
Převést nápad do strukturovaného issue vhodného pro backlog refinement a správně ho zařadit do GF_AOS workflow.

## Postup
1. Rozhodni, zda je vhodnější template `Feature` nebo `Discovery`.
2. Sepiš issue v odpovídající struktuře template.
3. Odděl problém od navrhovaného řešení.
4. Popiš přínos, scope a otevřené otázky.
5. Nastav přesně 1 `Lane *` a 1 `Type *`.
6. Prioritu navrhni konzervativně.

## Rozhodování
- nový build / capability / delivery item → `Feature`
- nejasný směr / otázka / audit / potřebné rozhodnutí → `Discovery`
- pokud nejsou jasné hranice scope, preferuj `Discovery`

## Lane
- dobře definovaný návrh → `Lane Ready`
- nejasný návrh / nutná validace → `Lane Discovery`
- validní, ale neaktuální nápad → `Lane Later`
- `Lane Now` nikdy automaticky

## Type
- nová schopnost → `Type Feature`
- otevřená otázka / epic / audit → `Type Discovery`
- pokud issue obsahuje otevřené otázky před implementací, použij `Type Discovery`

## Triage routing
- `Lane Ready` → do Triage review
- `Lane Discovery` → do Triage review
- `Lane Later` → může rovnou do backlogu

## Výstup
Použij strukturu:
### Cíl
### Uživatel / segment
### Problém
### Přínos
### Návrh scope
### Rizika / závislosti
### Otevřené otázky
### Lane
### Type
### Doporučená priorita
