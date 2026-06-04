---
name: Triage issue
description: Přiřazuje každou issue jediný Lane a Type, doporučí další krok a prioritu
scope: linear-workflow
---

Při triage issue pro GF_AOS se vždy řiď team docs jako source of truth:
- Final Issue Policy
- Automation Spec
- Short Agent Guidance
- Template Selection Rules

## Cíl
Připravit rychlé a použitelné triage rozhodnutí bez rozbití GF_AOS workflow modelu.

## Povinný model
Každé issue musí mít:
- přesně 1 `Lane *`
- přesně 1 `Type *`
- volitelné domain labels
- prioritu

Používej jen:
- `Lane Now`, `Lane Ready`, `Lane Discovery`, `Lane Later`
- `Type Bug`, `Type Feature`, `Type Discovery`, `Type Follow-up`, `Type Tech Debt`

Nikdy nepoužívej:
- `triage:*`
- starý `ready`
- více lane labelů
- více type labelů

## Postup
1. Shrň podstatu issue jednou až dvěma větami.
2. Rozhodni správný `Type *`.
3. Rozhodni správný `Lane *`.
4. Navrhni další krok.
5. Posuď, zda issue musí do Triage review nebo může rovnou do backlogu.
6. Navrhni konzervativní prioritu.
7. Vypiš chybějící informace.

## Type pravidla
- broken behavior / regression / wrong behavior → `Type Bug`
- nová schopnost / delivery item → `Type Feature`
- výzkum / epic / arch rozhodnutí / audit / otevřená otázka → `Type Discovery`
- navazuje na review nebo dřívější issue → `Type Follow-up`
- refactor / cleanup / infra hardening / maintainability → `Type Tech Debt`
- pokud issue obsahuje otevřené otázky, audit nebo rozhodnutí před implementací, použij `Type Discovery` i když technicky souvisí s cleanupem nebo hardeningem

## Lane pravidla
- implementovatelná a konkrétní práce → `Lane Ready`
- nejasný scope / potřeba rozhodnutí → `Lane Discovery`
- validní, ale neaktuální práce → `Lane Later`
- `Lane Now` nikdy nenastavuj automaticky

## Triage routing
- `Lane Ready` → issue má jít do Triage review
- `Lane Discovery` → issue má jít do Triage review
- `Lane Later` → může jít rovnou do backlogu

## Priority
- `Urgent` jen pro security, data loss, hard blocker
- `High` pro jasný release nebo delivery blocker
- jinak buď konzervativní: `Medium`, `Low`, `No priority`

## Výstup
Použij strukturu:
### Shrnutí
### Type
### Lane
### Doporučení
### Triage routing
### Chybějící informace
### Doporučená priorita

Piš stručně, rozhodovacím jazykem a nevymýšlej detaily bez označení nejistoty.
