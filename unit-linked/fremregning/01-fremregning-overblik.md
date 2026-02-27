# Fremregning af Unit-Linked Policer – Overblik

## 1. Hvad er fremregning?

**Fremregning** (engelsk: *projection* eller *policy projection*) er beregningen af en forsikringspolices forventede fremtidige værdier. For en unit-linked police beregnes typisk:

- Forventet depotværdi på et fremtidigt tidspunkt
- Forventede udbetalinger (pension, dødsfald, invaliditet)
- Fripoliceværdier ved præmieophør
- Kontantværdier ved tilbagekøb

Fremregning bruges til:
1. **Kundekommunikation** – lovpligtige pensionsoverslag og prognoser
2. **Aktuarmæssige beregninger** – hensættelsesberegning og solvens
3. **Profitanalyse** – embedded value og value of new business
4. **ALM** – asset/liability management

---

## 2. Grundlæggende fremregningsmodel

### 2.1 Depotfremregning (deterministisk)

For et givet scenarie med afkast `r(t)` fremregnes depotet:

```
D(t+1) = D(t) × (1 + r(t)) + P(t) − C_adm(t) − C_forsikring(t)
```

Hvor:
- `D(t)` = Depotværdi ved tidspunkt t
- `r(t)` = Investeringsafkast i perioden [t, t+1]
- `P(t)` = Præmieindbetalinger i perioden
- `C_adm(t)` = Administrationsomkostninger trukket fra depotet
- `C_forsikring(t)` = Forsikringsomkostninger (COI – Cost of Insurance)

### 2.2 Stokastisk fremregning

I stokastiske modeller simuleres mange mulige scenarier for afkastet:

```
r(t) ~ Stokastisk afkastmodel (fx GBM, Black-Scholes, scenarietræ)
```

Resultaterne præsenteres som:
- Forventede værdier (middelscenarie)
- Percentiler (fx 10%, 25%, 50%, 75%, 90%)
- Worst-case og best-case scenarier

---

## 3. Lovpligtige pensionsoverslag (pensionsoverslagsbekendtgørelsen)

### 3.1 Regulatorisk krav

Ifølge **Bekendtgørelse om god skik for finansielle virksomheder** og den tilhørende **pensionsoverslagsbekendtgørelse** skal forsikringsselskaber udarbejde pensionsoverslag til forsikringstagere.

**Pensionsinfo** (www.pensionsinfo.dk) er den fælles platform, der aggregerer overslag fra alle selskaber.

### 3.2 Scenariekrav

Pensionsoverslag for markedsrenteprodukter skal beregnes med:

| Scenarie | Beskrivelse |
|----------|-------------|
| **Lavt** | Konservativt afkastscenarie |
| **Middel** | Forventet afkastscenarie |
| **Højt** | Optimistisk afkastscenarie |

Scenarierne fastsættes typisk af **Forsikring & Pension** (brancheorganisationen) som vejledende satser.

### 3.3 Vejledende afkastforudsætninger (Forsikring & Pension)

Forsikring & Pension udgiver løbende vejledende forudsætninger. Eksempel på typiske satser (aktieandel og obligationsandel):

| Aktivklasse | Lavt scenarie | Middel scenarie | Højt scenarie |
|-------------|---------------|-----------------|---------------|
| Globale aktier | ~2% p.a. | ~6-7% p.a. | ~11-12% p.a. |
| Obligationer | ~0-1% p.a. | ~2-3% p.a. | ~4-5% p.a. |
| Ejendomme | ~2% p.a. | ~5% p.a. | ~8% p.a. |

*Bemærk: De faktiske satser opdateres løbende – se Forsikring & Pensions seneste vejledning.*

---

## 4. Fremregningskomponenter

### 4.1 Afkast

Det forventede afkast afhænger af:
- **Aktivallokering** i den valgte investeringsprofil
- **Investeringsomkostninger** (ÅOP – Årlige Omkostninger i Procent)
- **Skatter** (PAL-skat på 15,3% for pensionsordninger)

Netto-afkast efter skat og omkostninger:
```
r_netto = r_brutto × (1 - PAL-sats) - ÅOP
```

### 4.2 Præmier

Præmieinput til fremregningen:
- **Fast præmie**: Konstant nominelt beløb
- **Indeksregulering**: Præmien stiger med lønindeks eller fast procent
- **Variable præmier**: Arbejdsgiverbidrag, ATP-bidrag mv.

### 4.3 Administrationsomkostninger

Tre typer administrationsomkostninger:

| Type | Beregningsgrundlag | Typisk sats |
|------|-------------------|-------------|
| **Depotgebyr** | % af depotværdi | 0,1 – 0,5% p.a. |
| **Præmiegebyr** | % af præmie | 0 – 5% |
| **Fast gebyr** | Kr. pr. år | 0 – 500 kr. |

### 4.4 Forsikringsomkostninger

Omkostninger til dækning af biometriske risici:

**Dødsfaldsdækning:**
```
COI_død(t) = max(0, Forsikringssum − D(t)) × q_x(t) / 12
```

**Invaliditetsdækning:**
```
COI_invalid(t) = Dækningsbeløb × i_x(t) / 12
```

Hvor `q_x` og `i_x` er biometriske intensiteter fra det tekniske grundlag.

---

## 5. Fripolice og kontantværdi

### 5.1 Fripoliceværdi

Ved præmieophør omdannes policen til en fripolice. Fripoliceværdien er:

```
Fripoliceværdi = Depotværdi på ophørstidspunktet
```

For unit-linked er dette simpelt, da der ikke er nogen traditionel fripoliceberegning – depotet forbliver investeret.

Dog reduceres forsikringssummer proportionalt:
```
Ny forsikringssum = Gammel sum × (Fripoliceværdi / Hensættelse ved fuld præmiebetaling)
```

### 5.2 Kontantværdi (tilbagekøb)

```
Kontantværdi = Depotværdi − Eventuelle tilbagekøbsfradrag
```

For mange moderne unit-linked produkter er der ingen tilbagekøbsfradrag (0 kr. i fradrag).

---

## 6. Fremregning til pensionering

### 6.1 Akkumulationsfase

Fra indgåelsestidspunkt til pensioneringstidspunkt:

```
D(T_pension) = D(0) × ∏(1 + r(t)) + Σ[P(t) − C(t)] × ∏(1 + r(s))
```

### 6.2 Udbetaling – livrente

Ved pensionering konverteres depotet til en livrente. Konverteringsfaktoren afhænger af:

- Forsikringstagers alder og køn ved pensionering
- Aktuelt renteniveau på konverteringstidspunktet
- Valgt livrenteform (livsvarig, ophørende, ægtefælledækning mv.)

**Konversionsfaktor:**
```
Månedlig livrente = D(T_pension) / a_x(T_pension, r)
```

Hvor `a_x(r)` er den aktuarmæssige annuitetsfaktor ved rente `r` og alder `x`.

For unit-linked livrenter er udbetalingen variabel og afhænger af det fortsatte investeringsafkast.

### 6.3 Udbetaling – ratepension

Ratepensionen udbetales over en fast årrække (min. 10 år):

```
Månedlig rate(t) = D(t) / Resterende_antal_måneder
```

Ved unit-linked ratepension varierer de månedlige udbetalinger med investeringsafkastet.
