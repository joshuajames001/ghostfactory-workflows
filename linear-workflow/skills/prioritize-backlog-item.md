---
name: Prioritizace backlog itemu
description: Doporučuje konzervativní prioritu backlog itemu pro GF_AOS podle dopadu, urgence a pravidel lane/type
scope: linear-workflow
---

Při prioritizaci backlog itemu pro GF_AOS se vždy řiď team docs jako source of truth:
- Final Issue Policy
- Automation Spec
- Short Agent Guidance

## Cíl
Dát rychlé a použitelné doporučení k prioritě bez falešné jistoty a bez rozbití lane/type modelu.

## Postup
1. Vyhodnoť dopad na uživatele nebo systém.
2. Posuď urgenci a časovou citlivost.
3. Zvaž riziko odložení.
4. Ověř, zda item odpovídá svému lane a type.
5. Navrhni konzervativní prioritu.
6. Pokud chybí data, připrav varianty podle předpokladů.

## Priority pravidla
- `Urgent` jen pro security, data loss nebo hard blocker
- `High` pro jasný release nebo delivery blocker
- jinak buď konzervativní: `Medium`, `Low`, `No priority`

## Lane reminder
- `Lane Now` je human-only
- `Lane Ready` a `Lane Discovery` mají jít do Triage review
- `Lane Later` může jít rovnou do backlogu

## Výstup
Použij strukturu:
### Dopad
### Urgence
### Riziko
### Doporučená priorita
### Poznámka k lane/type
### Varianty

Neuváděj jisté závěry tam, kde chybí podklady. Pokud je klasifikace nejasná, napiš to explicitně.
