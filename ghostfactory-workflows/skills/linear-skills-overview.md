# GF_AOS Skills Overview

Přehled aktuálních osobních skills používaných pro práci v Linearu a návazném AI-first workflow.

Tento soubor slouží jako sdílitelný přehled pro komunitu a jako reference k tomu, jaké reusable workflows byly v rámci GF_AOS nastaveny.

---

## Stav

### Plně sladěné s novým GF_AOS issue modelem
Tyto skills počítají s:
- `Lane Now / Ready / Discovery / Later`
- `Type Bug / Feature / Discovery / Follow-up / Tech Debt`
- zákazem `triage:*`
- zákazem starého `ready`
- hybridním modelem:
  - `Lane Ready` a `Lane Discovery` → Triage review
  - `Lane Later` → může rovnou do backlogu

### Obecné / neutrální skills
Tyto skills nejsou přímo navázané na issue intake klasifikaci, takže zůstávají použitelné i bez přepisu.

---

# 1. Skills sladěné s novým GF_AOS modelem

## Create GF issues
**Účel:** vytváření nových issue pro GF_AOS podle team policy, template rules a nového lane/type modelu.

**Použití:**
- session review
- nové issue z Claude
- ruční create issue flow

**Klíčové vlastnosti:**
- vybírá správný template
- nastavuje 1× lane a 1× type
- konzervativně zachází s prioritou
- umí rozlišit `Type Discovery` vs `Type Tech Debt`
- počítá s tím, že issue od Claude často nejdou automaticky přes Triage

---

## Triage issue
**Účel:** rychlé triage rozhodnutí nad issue podle nového GF_AOS modelu.

**Použití:**
- zhodnocení nového issue
- rozhodnutí o lane/type
- doporučení dalšího kroku

**Klíčové vlastnosti:**
- vrací shrnutí, doporučení, lane, type a priority návrh
- počítá s Triage checkpointem pro `Lane Ready` a `Lane Discovery`

---

## Prioritizace backlog itemu
**Účel:** vyhodnotit dopad, urgenci a riziko backlog itemu bez falešné jistoty.

**Použití:**
- backlog review
- rozhodnutí mezi Medium / Low / No priority
- kontrola, zda se priority nepřestřelují

**Klíčové vlastnosti:**
- konzervativní práce s prioritou
- respektuje lane/type model
- neeskaluje automaticky bez silného důvodu

---

## Feature request do backlogu
**Účel:** převést nápad do backlog issue vhodného pro planning a prioritizaci.

**Použití:**
- nový feature request
- product idea
- capability návrh

**Klíčové vlastnosti:**
- rozlišuje Feature vs Discovery
- používá správný template
- vrací lane/type + prioritní doporučení

---

## Bug report z poznámek
**Účel:** převést neformální poznámky nebo chat do kvalitního bug issue.

**Použití:**
- incidenty
- regression reporty
- technické poznámky o chybách

**Klíčové vlastnosti:**
- používá Bug template
- odděluje expected vs actual
- umí rozhodnout mezi `Type Bug` a `Type Discovery`, pokud ještě chybí příčina

---

## Issue z neformálního zadání
**Účel:** převést neformální popis do správně strukturovaného issue.

**Použití:**
- kusé zadání
- nápady z poznámek
- technické úkoly bez struktury

**Klíčové vlastnosti:**
- vybírá správný template
- vrací lane/type
- respektuje GF_AOS policy

---

## Backlog grooming
**Účel:** ověřit kvalitu backlog itemu a připravenost pro další krok.

**Použití:**
- backlog cleanup
- refinement readiness
- kontrola klasifikace

**Klíčové vlastnosti:**
- kontroluje, zda issue má správný lane/type
- odhaluje missing info, rizika a závislosti
- umí doporučit přesun mezi `Lane Ready`, `Lane Discovery`, `Lane Later`

---

# 2. Obecné / neutrální skills

## PRD nebo note do issue tree
**Účel:** převést PRD nebo větší poznámky do issue tree s workstreamy a závislostmi.

**Poznámka:**
Není přímo navázaný na issue intake model. Později může být rozšířen o automatické přiřazení lane/type jednotlivým issue.

---

## Spec z issue do implementace
**Účel:** převést issue do implementační specifikace s kroky, požadavky a riziky.

**Poznámka:**
Workflow-safe. Není potřeba urgentní úprava.

---

## Release notes
**Účel:** připravit stručné release notes a shrnutí změn.

**Poznámka:**
Není v konfliktu s issue modelem.

---

## Technické zadání pro AI nebo integraci
**Účel:** převést business požadavek do technického zadání pro AI/integraci.

**Poznámka:**
Obecný skill, použitelný dál beze změn.

---

## Týdenní update projektu
**Účel:** sepsat krátký update projektu se změnami, riziky a dalšími kroky.

**Poznámka:**
Není závislý na lane/type issue modelu.

---

## Shrnutí diskuze do rozhodnutí
**Účel:** převést průběžnou diskuzi do strukturovaného rozhodnutí.

**Poznámka:**
Obecný, workflow-safe skill.

---

# 3. Doporučené použití v praxi

## Pro session review
Používej hlavně:
- `Create GF issues`
- `Bug report z poznámek`
- `Feature request do backlogu`
- `Issue z neformálního zadání`

## Pro backlog hygiene
Používej:
- `Triage issue`
- `Backlog grooming`
- `Prioritizace backlog itemu`

## Pro větší rozpad práce
Používej:
- `PRD nebo note do issue tree`
- `Spec z issue do implementace`

## Pro komunikaci a reporting
Používej:
- `Týdenní update projektu`
- `Shrnutí diskuze do rozhodnutí`
- `Release notes`

---

# 4. Doporučená architektura workflow

## Linear jako control plane
Linear drží:
- intake
- triage
- backlog
- planning
- execution handoff

## Claude / externí agent jako operator
Claude pomáhá s:
- tvorbou issue
- prvotní klasifikací
- rozpadáním zadání
- převodem poznámek do struktury

## Člověk jako finální rozhodnutí
Člověk drží:
- `Lane Now`
- cycle selection
- finální priority override
- review checkpoint u `Lane Ready` a `Lane Discovery`

---

# 5. Shrnutí

GF_AOS skills nejsou jen prompty. Jsou to malé operační workflow moduly pro AI-first práci v Linearu.

Nejdůležitější vrstva je ta, která vytváří a třídí issue. Ta byla sjednocena na:
- Templates → dávají strukturu
- Lane → říká, kdy a jak se má issue řešit
- Type → říká, o jaký typ práce jde
- Triage → druhá kontrola pro issue s vyšším rozhodovacím rizikem

Tento model je dobře přenositelný i do jiných AI-assisted týmů, kde issue často nevznikají ručně, ale přes agenty.
