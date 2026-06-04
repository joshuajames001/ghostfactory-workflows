# Linear for AI-First Issue Workflows

Praktický tutorial pro solo founder / AI-first product-development workflow nad Linearem, kde issue často vytváří Claude nebo jiný agent.

---

## Problém, který řešíme

Typický problém v AI-assisted workflow:

- proběhne session review
- z review vzniknou nové issue
- v dalším sprintu se řeší tyto issue
- při řešení vzniknou další issue
- backlog bobtná a člověk má pocit, že se točí na místě

Další komplikace:

- issue často nevznikají ručně v Linearu, ale přes externího agenta (např. Claude)
- pokud issue nejdou přes Triage, team Triage automations se nespustí
- pokud není sjednocené schema labels / lane / type, agenti rychle vyrábějí nekonzistentní backlog

Cíl je udělat z Linearu **control plane**, ne jen místo, kam padají tasky.

---

## Hlavní princip

Linear má být:

- source of truth pro planning
- source of truth pro triage
- source of truth pro backlog hygiene
- source of truth pro execution handoff

Agenti nejsou source of truth.
Agenti mají:

- pomáhat se strukturou
- pomáhat s klasifikací
- pomáhat s vytvářením issue
- ale ne určovat aktivní práci bez review

---

## Důležité zjištění: Triage není univerzální spouštěč

V Linearu se Triage nespouští periodicky.
Triage funguje **událostně** — když issue **vstoupí do Triage**.

To znamená:

- issue vytvořená integrací nebo mimo team může skončit v Triage
- issue vytvořená přímo jako normální team issue do backlogu nemusí do Triage vůbec jít

Praktický důsledek:

Pokud issue vytváří Claude mimo Linear Agent chat a nevkládá je do Triage, pak se nespustí:

- Triage Intelligence
- Triage Rules
- Agent Automations navázané na „when issue enters triage“

Proto je nutné mít dvojí model:

1. **Claude-created issues** musí být vytvořená už rovnou správně
2. **Triage** slouží jako review checkpoint pro případy, které do něj skutečně vstoupí nebo které tam vědomě pošleš

---

## Finální issue schema pro tým GF_AOS

Každé issue má mít:

- přesně **1 Lane**
- přesně **1 Type**
- volitelné domain labels
- prioritu

### Lane labels

Používat jen:

- `Lane Now`
- `Lane Ready`
- `Lane Discovery`
- `Lane Later`

### Význam lane

- `Lane Now`
  - aktivně řešené teď
  - jen ruční rozhodnutí člověka

- `Lane Ready`
  - konkrétní, implementovatelné, připravené pro planning
  - u AI-generated issue má jít přes review checkpoint

- `Lane Discovery`
  - je potřeba rozhodnutí, validace nebo rozpad scope
  - má jít přes review checkpoint

- `Lane Later`
  - validní práce, ale ne teď
  - může jít rovnou do backlogu

### Type labels

Používat jen:

- `Type Bug`
- `Type Feature`
- `Type Discovery`
- `Type Follow-up`
- `Type Tech Debt`

### Význam type

- `Type Bug`
  - broken behavior, regression, wrong behavior

- `Type Feature`
  - nová schopnost nebo delivery item

- `Type Discovery`
  - průzkum, epic, audit, arch rozhodnutí, otevřená otázka

- `Type Follow-up`
  - navazující práce po review nebo po hotovém issue

- `Type Tech Debt`
  - refactor, cleanup, infra hardening, maintainability

### Zakázané labely

Nepoužívat jako workflow model:

- `triage:*`
- starý `ready`

---

## Klíčové pravidlo, které se ukázalo jako důležité

Pokud issue obsahuje:

- otevřené otázky
- audit
- nutné rozhodnutí před implementací

pak má být:

- `Type Discovery`

**i když technicky souvisí s cleanupem nebo hardeningem**.

Tohle je důležité, protože bez tohoto pravidla mají agenti tendenci cpát „decision-first“ issue do `Type Tech Debt`.

---

## Hybridní model pro AI-generated issues

Ne všechno musí přes Triage, jinak vzniká zbytečný overhead.

### Doporučený model

- `Lane Discovery` → pošli do **Triage**
- `Lane Ready` → pošli do **Triage**
- `Lane Later` → může jít rovnou do **backlogu**
- `Lane Now` → agent nikdy nenastavuje

### Proč to dává smysl

`Lane Ready` a `Lane Discovery` jsou issue, která mají dopad na blízkou práci nebo vyžadují rozhodnutí.
Tady chceš explicitní checkpoint.

`Lane Later` jsou low-risk backlog items, kde review moment není tak důležitý.

---

## Co z toho plyne pro Claude-created issues

Protože issue budou často vytvářet externí agenti a ne Linear Agent v Triage flow, musí být Claude naučen:

- vybrat správný template
- napsat issue ve správné struktuře
- nastavit správný lane
- nastavit správný type
- být konzervativní s prioritou

Nesmíš spoléhat, že to za něj „někde potom opraví Triage“.

---

## Templates nejsou náhrada za triage

Templates slouží jako **structured intake**.
To znamená:

- zvyšují kvalitu vstupu
- zlepšují rozhodování agenta i triage
- drží konzistenci popisu issue

Templates samy o sobě nerozhodnou:

- co je důležité
- co má být `Lane Ready`
- co je `Type Discovery`

Ale výrazně tomu pomáhají.

---

## Doporučené issue templates

### 1. Bug
Použij, když:

- něco je rozbité
- jde o regression
- existuje expected vs actual behavior

Struktura:

```md
## What happened

## Why it matters

## Expected behavior

## Actual behavior

## Impact

## Acceptance criteria
- [ ]
- [ ]
- [ ]

## Related issue / review context
```

---

### 2. Feature
Použij, když:

- přidáváš novou schopnost
- dodáváš nový screen, API, workflow nebo delivery item

Struktura:

```md
## Kontext

## Cíl

## Scope
- 
- 
- 

## Out of scope
- 
- 

## Acceptance criteria
- [ ]
- [ ]
- [ ]
```

---

### 3. Discovery
Použij, když:

- cílem ještě není implementace
- chybí rozhodnutí
- jde o architekturu, audit, epic nebo otevřenou otázku

Struktura:

```md
## Kontext

## Problém / otázka

## Možné směry
- 
- 
- 

## Exit criteria
- [ ] máme doporučené rozhodnutí
- [ ] máme důvod proč
- [ ] máme jasný next step

## Zdroj / reference
```

---

### 4. Follow-up
Použij, když:

- issue vzniká z review
- navazuje na hotovou práci
- explicitně chceš zachovat návaznost

Struktura:

```md
## What

## Why

## Řešení

## Acceptance criteria
- [ ]
- [ ]
- [ ]

## Kontext
```

---

### 5. Tech Debt
Použij, když:

- jde o cleanup, refactor, hardening nebo maintainability
- nejde primárně o novou schopnost

Struktura:

```md
## Problém

## Řešení

## Done When
- [ ]
- [ ]
- [ ]

## Poznámka
```

---

## Template selection rules

Použij tento jednoduchý mapping:

- broken behavior → **Bug**
- new capability → **Feature**
- not enough clarity / audit / need decision → **Discovery**
- came from previous issue or review → **Follow-up**
- cleanup / refactor / hardening without open decision → **Tech Debt**

---

## Priority pravidla

Priority má agent navrhovat konzervativně.

### Bezpečné pravidlo

- `Urgent`
  - security
  - data loss
  - hard blocker

- `High`
  - release blocker
  - významný delivery blocker

- jinak:
  - `Medium`
  - `Low`
  - `No priority`

A stále platí:

- `Lane Now` nikdy agent nenastavuje
- cycle selection je ruční rozhodnutí člověka

---

## K čemu je Triage v AI workflow skutečně dobrá

Triage je užitečná jako:

- explicitní review checkpoint
- místo, kde opravíš špatně zadaný lane/type/priority
- ochrana před tím, aby se špatně klasifikovaná AI issue ztratila v backlogu

Pro AI-generated issue má tedy smysl hlavně tam, kde:

- je `Lane Ready`
- je `Lane Discovery`

To je přesně ten okamžik, kdy chceš druhou kontrolu.

---

## Co bylo potřeba v praxi uklidit

Při zavádění workflow se ukázaly typické problémy:

- dvojí lane model (`Lane *` vs `triage:*`)
- chybějící type labels
- starý `ready` label přežívající ve starých projektech
- agenti vytvářející issue mimo Triage
- nejasná hranice mezi `Type Discovery` a `Type Tech Debt`

Proto je důležité nejdřív:

1. sjednotit labels
2. vyčistit reprezentativní projekty
3. sepsat policy a guidance
4. vytvořit templates
5. teprve pak ladit automations a MCP workflows

---

## Doporučený rollout postup

### Fáze 1 — Team-level standard

Zaveď pro celý tým:

- `Lane *`
- `Type *`
- priority policy
- krátkou guidance
- automation spec

### Fáze 2 — Vyčištění klíčových projektů

Vyčisti několik reprezentativních projektů, aby vznikl reference model.

Např.:

- Span Chain / Observability Core
- RAG GF AOS
- GhostFactory AOS 3.0

### Fáze 3 — Templates

Zaveď issue templates:

- Bug
- Feature
- Discovery
- Follow-up
- Tech Debt

### Fáze 4 — Claude / agent skill

Vytvoř agent skill, který:

- načte team docs
- vybere správný template
- vytvoří issue už ve správném tvaru

### Fáze 5 — Ověření v praxi

Nejdřív testuj na reálných session reviews.
Teprve pak dolaďuj další projekty nebo pokročilejší MCP workflows.

---

## Doporučené rozdělení rolí

### Linear
- planning
- triage
- backlog organization
- execution handoff
- source of truth

### Claude / externí agent
- strukturované vytváření issue
- první klasifikace
- návrh priority
- follow-up generation

### Člověk
- `Lane Now`
- cycle selection
- priority override
- review checkpoint v Triage

---

## Doporučení natvrdo

Pokud issue vytváří převážně Claude:

- nespolehni se jen na Triage
- nauč Claude issue vytvářet správně už při vzniku
- ale zároveň použij Triage jako druhou kontrolu pro `Lane Ready` a `Lane Discovery`

To je nejpraktičtější hybridní model.

---

## Shrnutí v jedné větě

Nejlepší AI-first workflow v Linearu není „nechat agenta dělat všechno“, ale postavit systém, kde:

- templates dávají strukturu,
- agent dává první klasifikaci,
- triage dává checkpoint,
- a člověk rozhoduje o aktivní práci.
