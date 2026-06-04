---
name: Create GF issues
description: Create correctly labeled issues for GF_AOS with appropriate templates and conservative priority
scope: linear-workflow
---

Při vytváření issue pro GF_AOS se vždy řiď team docs jako source of truth:
- Final Issue Policy
- Automation Spec
- Short Agent Guidance
- Template Selection Rules

Před vytvořením issue nejdřív vyber správný issue template:
- Bug — broken behavior, regression, expected vs actual
- Feature — nová schopnost nebo delivery item
- Discovery — nejasný scope, otázka, epic, architektonické rozhodnutí
- Follow-up — práce vzniklá z review nebo navazující na hotové issue
- Tech Debt — refactor, cleanup, hardening, maintainability

Issue vytvoř rovnou správně, nespoléhej na Triage. Issue od Claude obvykle nevstupují do team Triage, takže lane a type musí být nastavené už při vytvoření.

Každé issue musí mít:
- přesně 1 `Lane *` label
- přesně 1 `Type *` label
- volitelné domain labels
- prioritu nastavenou konzervativně

Používej jen tyto lane labels:
- `Lane Now`
- `Lane Ready`
- `Lane Discovery`
- `Lane Later`

Používej jen tyto type labels:
- `Type Bug`
- `Type Feature`
- `Type Discovery`
- `Type Follow-up`
- `Type Tech Debt`

Nikdy nepoužívej:
- `triage:*`
- starý `ready`

Pravidla pro lane:
- `Lane Now` nikdy nenastavuj automaticky
- pokud je issue konkrétní a implementovatelné, použij `Lane Ready`
- pokud issue obsahuje otevřené otázky nebo potřebuje audit či rozhodnutí před implementací, použij `Lane Discovery`
- pokud je práce validní, ale neaktuální nebo odložená, použij `Lane Later`

Pravidla pro type:
- broken behavior / regression / wrong behavior → `Type Bug`
- nová schopnost / nový screen / API / workflow / delivery → `Type Feature`
- výzkum / epic / arch rozhodnutí / otevřená otázka → `Type Discovery`
- navazuje na review, retrospektivu nebo předchozí issue → `Type Follow-up`
- refactor / cleanup / infra hardening / maintainability → `Type Tech Debt`
- pokud issue obsahuje otevřené otázky, audit nebo rozhodnutí nutné před implementací, použij `Type Discovery`, i když technicky souvisí s cleanupem nebo hardeningem

Priority:
- `Urgent` jen pro security, data loss nebo hard blocker
- `High` pro jasný release nebo delivery blocker
- jinak buď konzervativní: `Medium`, `Low` nebo `No priority`
- prioritu nepřestřeluj

Při psaní issue používej strukturu odpovídající zvolenému template.

Pro Bug použij sekce:
- What happened
- Why it matters
- Expected behavior
- Actual behavior
- Impact
- Acceptance criteria
- Related issue / review context

Pro Feature použij sekce:
- Kontext
- Cíl
- Scope
- Out of scope
- Acceptance criteria

Pro Discovery použij sekce:
- Kontext
- Problém / otázka
- Možné směry
- Exit criteria
- Zdroj / reference

Pro Follow-up použij sekce:
- What
- Why
- Řešení
- Acceptance criteria
- Kontext

Pro Tech Debt použij sekce:
- Problém
- Řešení
- Done When
- Poznámka

Při session review:
- z každého bodu nejdřív rozhodni, jestli jde o Bug, Feature, Discovery, Follow-up nebo Tech Debt
- issue vytvářej jen tehdy, když je to skutečně samostatná práce
- pokud si nejsi jistý mezi `Lane Ready` a `Lane Discovery`, zvol `Lane Discovery`
- pokud si nejsi jistý mezi `Type Feature` a `Type Tech Debt`, zvaž, zda jde o novou schopnost nebo jen zlepšení implementace
- pokud si nejsi jistý mezi `Type Tech Debt` a `Type Discovery`, a issue obsahuje otevřené otázky, audit nebo rozhodnutí před implementací, zvol `Type Discovery`

Cílem je, aby nové issue byly vytvořené rovnou ve správném tvaru a bez potřeby dodatečné triage opravy.
