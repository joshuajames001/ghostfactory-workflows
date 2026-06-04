# Final Issue Policy (template)

Finální operativní policy pro tým `<TEAM>`. Kanonický zdroj pravdy pro klasifikaci issue — skills i automations se odkazují sem.

## 1. Povinné klasifikační osy
Každé nové issue má mít:
- **1× Lane**
- **1× Type**
- volitelně **0–3 domain labels**
- priority

## 2. Lane labels
Používat jen: `Lane Now`, `Lane Ready`, `Lane Discovery`, `Lane Later`

### Pravidla
- issue nesmí mít víc než jeden lane label
- `Lane Now` se nenastavuje automaticky
- při nejistotě: `Lane Discovery` (ne `Lane Ready`)

### Význam
- `Lane Now` — aktivně řešené teď
- `Lane Ready` — konkrétní, implementovatelné, připravené pro planning; před backlogem projít Triage review
- `Lane Discovery` — potřebuje rozhodnutí, validaci nebo rozpad; projít Triage
- `Lane Later` — validní práce, ale ne teď; může rovnou do backlogu

## 3. Type labels
Používat jen: `Type Bug`, `Type Feature`, `Type Discovery`, `Type Follow-up`, `Type Tech Debt`

### Pravidla
- issue nesmí být bez type ani mít víc než jeden type

### Význam
- `Type Bug` — chyba, regression, nesprávné chování
- `Type Feature` — nová schopnost nebo dodávka hodnoty
- `Type Discovery` — cílem je rozhodnutí, ne implementace
- `Type Follow-up` — navazuje na hotovou práci, review nebo předchozí issue
- `Type Tech Debt` — refactor, cleanup, infra hardening, maintainability

## 4. Domain labels
Team-level, použité jen kde dávají smysl.
- **Common:** `Frontend`, `Backend`, `infra`, `Security`, `Testing`, `sdk`
- **Project-specific:** `<DOMAIN_LABEL>` dle projektu

> Example (GhostFactory) — Span Chain: `ledger`, `otel`, `evals`, `runtime`, `observability`, `liveview`, `scale`, `versioning`

Pravidla: domain label není lane ani type; max 3 na issue.

## 5. Priority policy
`Urgent` / `High` / `Medium` / `Low` / `No priority`
- agent může priority **navrhovat**
- automaticky nastavovat jen u jasných případů: security, data loss, hard blocker
- `Lane Now` a cycle vybírá člověk
- `Lane Ready` / `Lane Discovery` projdou Triage review → priorita se opraví dřív, než issue zapadne

## 6. Zakázané věci
- `triage:*` jako klasifikační model místo `Lane *`
- starý `ready` jako workflow label
- issue bez lane / bez type
- víc lane nebo víc type labelů najednou

## 7. Default behavior pro triage
**Lane:** konkrétní → `Lane Ready` · nejasné → `Lane Discovery` · validní odložené → `Lane Later`
**Type:** bug → `Type Bug` · nový build/delivery → `Type Feature` · arch/epic/průzkum → `Type Discovery` · navazující → `Type Follow-up` · refactor/cleanup → `Type Tech Debt`
**Routing:** `Lane Discovery` a `Lane Ready` → do Triage · `Lane Later` → rovnou backlog · `Lane Now` → jen ručně

## 8. Agent-generated issues
Issue od Claude / agenta = AI-generated intake:
- `Lane Ready` a `Lane Discovery` nejsou finálně schválené jen proto, že je agent nastavil
- Triage je explicitní review checkpoint před vstupem do backlogu (druhá kontrola routingu, typu i priority)

## 9. Hybrid model (praktický krok)
- templates = strukturovaný vstup
- agent = první klasifikace
- triage = review checkpoint pro `Lane Ready` a `Lane Discovery`
- backlog = až po přijetí v Triage, nebo rovnou jen pro `Lane Later`
