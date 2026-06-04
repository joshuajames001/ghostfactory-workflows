# Template Selection Rules (template)

Pravidla pro výběr issue template v týmu `<TEAM>`. Template nezajišťuje finální triage, ale výrazně zlepšuje kvalitu rozhodování. Viz [`../templates/`](../templates/).

## 1. Bug
Použij, když: něco je rozbité, regression, systém se chová jinak než má, existuje expected vs actual.
Mapuje na: `Type Bug` · `Lane Ready` (jasné co opravit) nebo `Lane Discovery` (nutné nejdřív zjistit příčinu) → do Triage.

## 2. Feature
Použij, když: přidáváš novou schopnost / screen / API / workflow / produktovou hodnotu a scope míří na implementation.
Mapuje na: `Type Feature` · `Lane Ready` (→ Triage review) nebo `Lane Later` (validní, ale ne teď).

## 3. Discovery
Použij, když: cílem ještě není implementace, chybí rozhodnutí, řešíš architekturu/varianty/nejasný scope, je to epic, audit nebo výzkumná otázka.
Mapuje na: `Type Discovery` · `Lane Discovery` → do Triage.

## 4. Follow-up
Použij, když: issue navazuje na review nebo předchozí hotovou práci, je to další krok mimo původní scope, chceš zachovat návaznost.
Mapuje na: `Type Follow-up` · `Lane Later` nebo `Lane Ready` (→ Triage).

## 5. Tech Debt
Použij, když: nejde primárně o novou schopnost, cílem je cleanup / refactor / maintainability / infra hardening.
Mapuje na: `Type Tech Debt` · `Lane Ready` (konkrétní) nebo `Lane Later`.
Pozor: pokud issue obsahuje otevřené otázky před implementací → není to Tech Debt, ale Discovery.

## Rychlé rozhodovací pravidlo
- broken behavior → **Bug**
- new capability → **Feature**
- not enough clarity / need decision / audit before action → **Discovery**
- came from previous issue/review → **Follow-up**
- cleanup / refactor / hardening without open decision → **Tech Debt**

## Priority & Triage reminder
- `Lane Now` nikdy automaticky; prioritu konzervativně; aktivní práci a cycle vybírá člověk
- AI-generated: `Lane Discovery` a `Lane Ready` → do Triage · `Lane Later` → rovnou backlog
