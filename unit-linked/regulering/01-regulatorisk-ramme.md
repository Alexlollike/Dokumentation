# Regulatorisk Ramme for Unit-Linked Forsikring i Danmark

## 1. Overordnet lovgivningsstruktur

Den regulatoriske ramme for unit-linked livsforsikring i Danmark er opbygget i lag:

```
EU-niveau
├── Solvens II-direktivet (2009/138/EF)
├── IORP II-direktivet (arbejdsmarkedspensioner)
├── IDD (Insurance Distribution Directive)
├── PRIIP-forordningen (nøgleinformationsdokumenter)
└── SFDR (Sustainable Finance Disclosure Regulation)

Dansk lovgivning
├── Lov om finansiel virksomhed (FIL)
├── Pensionsbeskatningsloven (PBL)
├── PAL-loven (pensionsafkastbeskatning)
├── Årsregnskabsloven (ÅRL)
└── Lov om firmapensionskasser

Bekendtgørelser (Finanstilsynet)
├── Bek. om livsforsikringsvirksomhed
├── Bek. om god skik for finansielle virksomheder
├── Pensionsoverslagsbekendtgørelsen
├── Bek. om finansielle rapporter for forsikringsselskaber
└── Bek. om opgørelse af SCR (Solvens II)
```

---

## 2. Solvens II (Direktiv 2009/138/EF)

### 2.1 Tre-søjlestruktur

**Søjle 1: Kvantitative krav**
- Minimumskapitalkrav (MCR – Minimum Capital Requirement)
- Solvenskapitalkrav (SCR – Solvency Capital Requirement)
- Beregning af tekniske hensættelser (Best Estimate + Risk Margin)
- Kapitalgrundlag (Own Funds) klassificeret i Tier 1, 2 og 3

**Søjle 2: Tilsynsmæssige krav**
- ORSA (Own Risk and Solvency Assessment)
- Governance-krav og fit & proper
- Ansvarshavende aktuar
- Intern revision og compliancefunktion

**Søjle 3: Rapporteringskrav**
- QRT (Quantitative Reporting Templates) til Finanstilsynet
- SFCR (Solvency and Financial Condition Report) – offentlig
- RSR (Regular Supervisory Report) – fortrolig

### 2.2 Tekniske hensættelser (Solvens II)

Tekniske hensættelser beregnes som:

```
Tekniske hensættelser = Best Estimate Liabilities (BEL) + Risikomargin (RM)
```

**For unit-linked policer:**

```
BEL_unit-linked = Depotværdi (markedsværdi) + BEL_forsikringsydelser
```

BEL for forsikringsydelserne:
```
BEL_forsikring = PV[fremtidige COI-cashflows] + PV[fremtidige administrationsomkostninger]
               - PV[fremtidige præmier]
```

Diskonteret med EIOPA's risikofrie rentekurve.

### 2.3 SCR – Standard Formula

SCR beregnes som VaR på 99,5%-niveau over 1 år:

```
SCR_basis = √(Σ Corr_ij × SCR_i × SCR_j)
```

Moduler for livsforsikringsselskaber:
- **SCR_mkt**: Markedsrisiko (aktier, renter, ejendomme, spread, valuta, koncentration)
- **SCR_life**: Livsforsikringsrisiko (dødelighed, levetid, invaliditet, katastrofe)
- **SCR_op**: Operationel risiko

For unit-linked:
- Markedsrisikoen bæres primært af forsikringstageren
- Dog bærer selskabet risiko ved:
  - Garantier (mindsteafkast, fripolicegarantier)
  - Fremtidige diskretionære fordele
  - Variabel-afgiftsindkomst (AUM-baserede gebyrer)

### 2.4 Look-through princippet

For unit-linked investeringer anvender Solvens II **look-through**:

Kapitalgrundlaget og SCR beregnes som om selskabet direkte ejer de underliggende aktiver, ikke blot andele i fonden.

```
SCR_unit-linked = Σ [Forsikringstagers andel × SCR_underliggende_aktiv]
```

---

## 3. Lov om finansiel virksomhed (FIL)

### 3.1 Relevante kapitler

- **Kapitel 1**: Definitioner – herunder definition af livsforsikringsklasser
- **Kapitel 9**: Tilladelse og drift af forsikringsselskaber
- **Kapitel 12**: Governance og ledelseskrav
- **Kapitel 13**: Kapitaldækning (Solvens II implementering)
- **Kapitel 22**: Kundeoplysningspligter og god skik

### 3.2 Forsikringsklasser (livsforsikring)

Livsforsikringsklasser relevante for unit-linked:

| Klasse | Beskrivelse |
|--------|-------------|
| **Klasse I** | Livsforsikring (dødsfald/overlevelse) |
| **Klasse III** | Unit-linked livsforsikring |
| **Klasse IV** | Permanent sygeforsikring |
| **Klasse V** | Tontiner |

**Klasse III** er den specifikke kategori for unit-linked:
- Forsikringstager bærer investeringsrisikoen
- Afkastet afhænger af investeringsenhedernes kursudvikling
- Særlige gennemsigtighedskrav

---

## 4. Pensionsbeskatningsloven (PBL)

### 4.1 Fradragsret

Indbetalinger til godkendte pensionsordninger giver fradrag:

| Ordningstype | Fradragsmaksimum (2024) | Fradragstype |
|-------------|------------------------|--------------|
| Ratepension | 63.100 kr./år | Fradrags (AM-bidrag og personskat) |
| Livrente med løbende udbetalinger | Ubegrænset | Fradrags |
| Kapitalpension (ophævet) | Ophævet | - |
| Aldersopsparing | 9.100 kr./år | Ikke fradrag, skattefri ved udbetaling |

### 4.2 Beskatning ved udbetaling

| Ordningstype | Beskatning |
|-------------|-----------|
| Ratepension | Personlig indkomst (op til ~55%) |
| Livrente | Personlig indkomst |
| Aldersopsparing | Skattefri |
| Ophævet pension (tidlig) | 60% skat |

### 4.3 Krav til godkendt pensionsordning

For at opnå fradragsret (§2-§14 PBL):
- Selskabet skal være godkendt af Finanstilsynet
- Policen skal opfylde krav til udbetalingstidspunkt
- Tilbagekøbsforbud i ophørsperiode (ratepension)

---

## 5. PAL-loven (Pensionsafkastbeskatningsloven)

### 5.1 Hvem er PAL-pligtige?

- Alle livsforsikringsselskaber for pensionsordninger under PBL §2-§12
- ATP og arbejdsmarkedspensionskasser
- **Ikke**: Frie midler (kapitalindkomst/aktieindkomst i stedet)

### 5.2 PAL-beregning for unit-linked

```
PAL-grundlag = Depotværdi(31/12) − Depotværdi(1/1) − Præmier + Udbetalinger
```

Eller mere præcist:

```
PAL-grundlag = Realiseret afkast + Urealiseret kursgevinst/-tab
             = (Udbytter + Realiserede kursgevinster) + ΔMarkedsværdi
```

PAL-sats: **15,3%**

### 5.3 Administration

- Selskabet beregner og indberetter PAL
- Betaling sker løbende (acontobetaling) og ved årsafslutning
- Underskud (negativ PAL) kan fremføres og modregnes

---

## 6. Pensionsoverslagsbekendtgørelsen

### 6.1 Formål

Bekendtgørelsen sikrer at forsikringstagere modtager ensartede og sammenlignelige pensionsoverslag.

### 6.2 Krav til pensionsoverslag

Hvert år skal forsikringstagere modtage (eller have adgang til) overslag der viser:

1. **Forventet pension** ved folkepensionsalderen
2. **Tre scenarier** (lav/middel/høj afkast)
3. **Forsikringsdækninger** (beløb ved invaliditet, dødsfald)
4. **Omkostningsinformation** (ÅOP)
5. **Fripoliceoplysninger** ved præmieophør

### 6.3 Forsikring & Pension's vejledende afkastforudsætninger

Forsikring & Pension publicerer løbende vejledende satser. Eksempel på struktur:

```
Afkastforudsætning = Risikofri rente + Risikopræmie − Investeringsomkostninger
```

Satser revideres typisk én gang om året, eller ved væsentlige markedsændringer.

---

## 7. IDD (Insurance Distribution Directive)

### 7.1 Krav til distribution

IDD (implementeret i dansk ret) kræver ved salg af unit-linked forsikringer:

- **Egnethedstest** (suitability assessment):
  - Kundens investeringserfaring og viden
  - Finansiel situation og risikovillighed
  - Investeringsmål og tidshorisont

- **PRIIPs KID** (Key Information Document):
  - Standardiseret 3-siders produktinformationsdokument
  - Beskriver risiko, afkast og omkostninger
  - Krav om performancescenarier

### 7.2 PRIIPs performancescenarier

For unit-linked produkter kræves 4 scenarier i KID:
- **Stress**: Worst-case scenarie
- **Ugunstigt**: 10.-percentil
- **Moderat**: 50.-percentil
- **Gunstigt**: 90.-percentil

Beregnes med specificeret metode (typisk historisk bootstrap eller parametrisk).

---

## 8. Finanstilsynets tilsyn

### 8.1 Tilsynsmodel

Finanstilsynet fører **risikobaseret tilsyn**:
- Selskaber vurderes på risikoprofil og kontrol
- Hyppigere tilsyn ved høj risiko
- PRISM (risikovurderingssystem)

### 8.2 Vigtige tilsynsaktiviteter

- Kvartalsvise QRT-indberetninger (Solvens II)
- Gennemgang af ORSA-rapport
- Inspektion af aktuarmæssige beregninger
- Tilsyn med god skik

### 8.3 Indgrebsmuligheder

- Påbud om kapitalindskud
- Forbud mod at indgå nye forsikringer
- Tilbagekaldelse af tilladelse (ultimativt)

---

## 9. SFDR (Sustainable Finance Disclosure Regulation)

### 9.1 Krav til bæredygtighedsoplysninger

SFDR kræver at finansielle produkter klassificeres:

| Artikel | Beskrivelse | Eksempel |
|---------|-------------|---------|
| **Art. 6** | Integrerer ikke bæredygtighedsrisici systematisk | Konventionelle produkter |
| **Art. 8** | Fremmer miljø/sociale karakteristika | "Lysegrønne" produkter |
| **Art. 9** | Har bæredygtigt investeringsmål | "Mørkegrønne" produkter |

**PFA Klima Plus**: Artikel 9
**Danica Bæredygtig**: Artikel 8/9
**Standard markedsrenteprodukter**: Typisk Artikel 8

### 9.2 Rapporteringskrav

Selskaberne skal publicere:
- SFDR-produktopplysninger (forud for tegning)
- Periodisk ESG-rapportering
- PAI (Principal Adverse Impact) indikatorer
