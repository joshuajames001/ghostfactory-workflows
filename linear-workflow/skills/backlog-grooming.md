---
name: Backlog grooming
description: Zajišťuje správné zařazení issue do GF_AOS modelu a zlepšuje její připravenost pro realizaci
scope: linear-workflow
---

Při backlog groomingu pro GF_AOS se vždy řiď team docs jako source of truth:
- Final Issue Policy
- Automation Spec
- Short Agent Guidance

## Cíl
Zvýšit kvalitu backlogu a ověřit, zda je issue správně zařazené podle nového GF_AOS modelu.

## Postup
1. Zkontroluj, zda má issue přesně 1 `Lane *` a 1 `Type *`.
2. Posuď, zda zvolený lane odpovídá stavu zadání.
3. Posuď, zda zvolený type odpovídá povaze práce.
4. Zkontroluj, zda jsou dostatečně konkrétní acceptance criteria nebo exit criteria.
5. Identifikuj chybějící rozhodnutí, závislosti a rizika.
6. Navrhni, zda issue zůstává `Lane Ready`, `Lane Discovery`, nebo `Lane Later`.

## Důležité pravidlo
Pokud issue obsahuje otevřené otázky, audit nebo rozhodnutí nutné před implementací, použij `Type Discovery` i když technicky souvisí s cleanupem nebo hardeningem.

## Triage routing
- `Lane Ready` → issue má jít do Triage review
- `Lane Discovery` → issue má jít do Triage review
- `Lane Later` → může zůstat přímo v backlogu
- `Lane Now` je human-only

## Výstup
Použij strukturu:
### Stav připravenosti
### Lane
### Type
### Co je v pořádku
### Co chybí
### Rizika a závislosti
### Doporučené úpravy

Piš stručně a akčně. Zaměř se na kvalitu zadání, ne na opis obsahu.
