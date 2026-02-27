# Regnskabsmæssig Behandling af Unit-Linked Forsikring

## 1. Regnskabsstandarder

Danske livsforsikringsselskaber kan aflægge regnskab efter:

| Standard | Anvendelse |
|----------|-----------|
| **Dansk GAAP (ÅRL)** | Alle selskaber (minimumsstandard) |
| **IFRS** | Selskaber noteret på fondsbørs eller ved frivillig valg |
| **Solvens II** | Tilsynsmæssig balance (parallel til regnskabet) |

De fleste danske livsforsikringsselskaber anvender **dansk GAAP** (Årsregnskabsloven + Finanstilsynets bekendtgørelse om finansielle rapporter).

---

## 2. Årsregnskabsloven og Finanstilsynets bekendtgørelse

### 2.1 Relevant lovgivning

- **ÅRL § 58-82**: Særlige bestemmelser for forsikringsselskaber
- **Bekendtgørelse nr. 937 af 27. november 2003** (med ændringer): Om finansielle rapporter for forsikringsselskaber og tværgående pensionskasser

### 2.2 Resultatopgørelse – format for livsforsikring

```
TEKNISK RESULTAT, LIVSFORSIKRING

Præmier, netto for genforsikring
  Bruttopræmier
  Afgivne genforsikringspræmier (−)

Investeringsafkast, overført fra ikke-teknisk konto
Investeringsafkast på henlæggelser for forsikringstagernes regning (unit-linked)

Erstatninger, netto for genforsikring
  Udbetalte erstatninger (brutto)
  Genforsikringsandel af udbetalte erstatninger (−)

Ændring i andre forsikringsmæssige hensættelser
  Livsforsikringshensættelse (ændring)
  Hensættelser for unit-linked kontrakter (ændring)

Forsikringsmæssige driftsomkostninger
Overført investeringsafkast (−)

TEKNISK RESULTAT I ALT
```

### 2.3 Balance – forsikringsmæssige hensættelser

```
PASSIVER

Forsikringsmæssige hensættelser
  A. Livsforsikringshensættelse
  B. Erstatningshensættelse
  C. Hensættelse for unit-linked kontrakter  ← CENTRAL POST
  D. Bonushensættelse
  E. Andre forsikringsmæssige hensættelser
```

**Hensættelse for unit-linked kontrakter** = Markedsværdi af de til forsikringstagerne tilhørende investeringer.

### 2.4 Aktiver – unit-linked investeringer

```
AKTIVER

Investeringsaktiver
  ...

Investeringsaktiver, forsikringstagernes risiko (unit-linked)
  Investeringsforeningsandele
  Obligationer
  Aktier
  Andre aktiver
```

Disse aktiver modsvares præcis af "Hensættelse for unit-linked kontrakter" på passivsiden.

---

## 3. Indregning og måling

### 3.1 Unit-linked investeringer

**Målingsprincip**: **Dagsværdi (fair value)**

- Børsnoterede værdipapirer: Officiel markedskurs
- Investeringsforeningsandele: Indre værdi (NAV)
- Ikke-noterede aktiver: Modelbaseret dagsværdi

Urealiserede kursgevinster/-tab indregnes direkte i **resultatopgørelsen** (ikke i anden totalindkomst).

### 3.2 Forsikringsmæssige hensættelser

**Hensættelse for unit-linked kontrakter** måles til:

```
Hensættelse = Markedsværdi af tilknyttede investeringsaktiver
```

Ændringen i hensættelsen indregnes i resultatopgørelsen under:
- **"Ændring i hensættelser for unit-linked kontrakter"**

### 3.3 Modregningsprincippet

Investeringsafkast og hensættelsesændring modsvarer hinanden:

```
Investeringsafkast, unit-linked: +100
Ændring i hensættelse, unit-linked: −100
Netto-effekt på resultat: 0
```

Det er kun **selskabets eget margin** (forsikringsomkostninger, gebyrindtægter) der påvirker teknisk resultat.

---

## 4. Præmier og erstatninger

### 4.1 Præmier

Bruttopræmier indregnes **periodiseret** til det regnskabsår de vedrører:

```
Periodiseret præmie = Indbetalt præmie + Skyldige præmier − Forudbetalte præmier
```

For unit-linked:
- Præmieindtægt = Modtagne præmier
- Hensættelsen stiger tilsvarende

### 4.2 Erstatninger

Udbetalte beløb ved:
- **Dødsfald**: Indregnes som erstatning ved udbetaling
- **Invaliditet**: Løbende ydelser indregnes som erstatning
- **Pension**: Løbende ydelser ved udbetaling

**Særligt for unit-linked**: Når depotet udbetales (fx ved dødsfald), falder hensættelsen tilsvarende – nettopåvirkning på resultat ≈ 0.

---

## 5. IFRS 17 – Insurance Contracts

### 5.1 Introduktion

IFRS 17 er den nye internationale regnskabsstandard for forsikringskontrakter, der erstatter IFRS 4. Ikrafttræden: **1. januar 2023** for IFRS-aflæggere.

### 5.2 Hovedmodeller under IFRS 17

| Model | Anvendelse |
|-------|-----------|
| **GMM** (General Measurement Model) | Standardmodel for alle forsikringskontrakter |
| **PAA** (Premium Allocation Approach) | Kortfristede kontrakter (<1 år) |
| **VFA** (Variable Fee Approach) | **Unit-linked og deltagelseskontrakter** |

### 5.3 VFA (Variable Fee Approach) for Unit-Linked

VFA er den relevante model for unit-linked kontrakter:

**Nøglebegreb: CSM (Contractual Service Margin)**

```
Forsikringskontraktens fulde regnskabsmæssige værdi:
= FCF (Fulfillment Cash Flows) + CSM
```

Hvor:
- **FCF** = PV[fremtidige cashflows] + Risikokorrigering
- **CSM** = Ikke-amortiseret fortjeneste fra fremtidigt servicelevering

**Under VFA justeres CSM for:**
- Ændring i dagsværdi af de underliggende poster (investeringer)
- Ændring i selskabets variable gebyr
- Effekt af optioner og garantier

### 5.4 VFA Cashflows

For unit-linked under VFA:

```
Fremtidige cashflows =
  Forsikringsomkostninger (COI, administration)
  − Fremtidige gebyrer (% af depot)
  + Garantiomkostninger (hvis nogen)
```

Disse diskonteres med **aktuarmæssig diskonteringsrente**.

### 5.5 P&L under IFRS 17 VFA

```
Forsikringsserviceresultat:
  CSM amortisering (frigivet tjeneste)
  + Erfaringsvarianter (actual vs expected)
  + Risikokorrigeringsændring

Forsikringsfinansieringsresultat:
  Rente på FCF
  Ændring i diskontseringsrente

Investeringsafkast:
  Faktisk afkast på unit-linked investeringer
```

---

## 6. Solvens II – Tilsynsmæssig balance

### 6.1 Forskel til regnskabsmæssig balance

Solvens II-balancen opgøres anderledes end ÅRL-balancen:

| Post | ÅRL | Solvens II |
|------|-----|-----------|
| Aktiver | Blandet (historisk kost + fair value) | Markedsværdi |
| Hensættelser | Bruttohensættelse | Best Estimate + Risikomargin |
| Egenkapital | Bogført egenkapital | Own Funds (Tier 1/2/3) |

### 6.2 Unit-linked under Solvens II

```
Tekniske hensættelser, unit-linked =
  Best Estimate (BEL)
  + Risikomargin (RM)
```

BEL for unit-linked:
```
BEL = Depotværdi + PV[fremtidige gebyrer og COI]
```

Risikomargin:
```
RM = 6% × PV[fremtidige SCR for ikke-afsikringsbare risici]
```

---

## 7. Nøgletal og ratioer i årsregnskaber

### 7.1 Standardiserede nøgletal (Finanstilsynets krav)

Forsikringsselskaber skal i årsrapporten inkludere:

| Nøgletal | Beregning |
|----------|-----------|
| **Afkastgrad** | Investeringsresultat / Gennemsnitlige investeringsaktiver |
| **Omkostningsprocent** | Driftsomkostninger / Præmier |
| **Erstatningsprocent** | Erstatninger / Præmier |
| **Kombineret ratio** | Erstatnings% + Omkostnings% |
| **Solvensgrad** | Kapitalgrundlag / Solvenskapitalkrav |

### 7.2 Unit-linked-specifikke nøgletal

| Nøgletal | Beskrivelse |
|----------|-------------|
| **AUM (Assets Under Management)** | Samlede unit-linked depoter |
| **Nettoindtegning** | Nye præmier − Ophørte policer |
| **Afkast, kundedepot** | Vægtet afkast på unit-linked depoter |
| **ÅOP** | Årlige omkostninger i procent |

---

## 8. Eksempel: Regnskabspost-flow for unit-linked

### Scenarie: Præmieindbetaling og afkast

```
Forsikringstager indbetaler 10.000 kr. i præmie:
  + Bruttopræmier: +10.000
  − Forsikringsomkostning (COI): −200
  − Administrationsomkostning: −50
  = Netto til depot: 9.750

Investeres i unit-linked fonde. Afkast 8% i perioden:
  + Investeringsafkast, forsikringstagers risiko: +780 (9.750 × 8%)
  − Ændring i hensættelse for unit-linked: −780

Netto-effekt på resultat fra investeringsafkast: 0

Teknisk resultat (selskabets margin):
  + Gebyrer (% af depot): +XX
  − Administrationsomkostninger: −XX
  = Teknisk resultat (margin)
```
