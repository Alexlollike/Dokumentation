# Embedded Value og Value of New Business

## 1. Hvad er Embedded Value?

**Embedded Value (EV)** er et aktuarmæssigt mål for værdien af et livsforsikringsselskabs eksisterende forsikringsportefølje. Det anvendes til:

- Intern ledelsesrapportering
- M&A-transaktioner (fusioner og opkøb)
- Investorkommunikation
- Præstationsmåling

### 1.1 Komponenter i Embedded Value

```
Embedded Value = Adjusted Net Worth (ANW) + Value of In-Force Business (VIF)
```

Hvor:
- **ANW** = Markedsværdi af kapitalgrundlag (fri kapital + kapital bundet i policer)
- **VIF** = Nutidsværdi af fremtidige overskud fra eksisterende portefølje

### 1.2 Value of New Business (VNB)

VNB måler værdien skabt ved nyindtegning i en given periode:

```
VNB = Nutidsværdi[fremtidige cashflows fra nye policer] ved tegning
```

---

## 2. Traditional Embedded Value (TEV)

### 2.1 Beregningsprincip

TEV anvender **deterministiske forudsætninger**:

```
VIF = PV[fremtidige overskud] − PV[kapitalomkostning]
```

Diskonteringsrente: **Risk discount rate (RDR)** – typisk 8-12% p.a. for livsforsikring

Svagheder:
- Ingen eksplicit håndtering af optioner og garantier
- Subjektiv valg af RDR
- Ikke markedskonsistent

---

## 3. Market Consistent Embedded Value (MCEV)

### 3.1 MCEV-principper (CFO Forum)

MCEV-principper (senest opdateret 2016) kræver:

- **Markedskonsistente** afkastforudsætninger
- Risikoneutral prissætning af optioner og garantier
- Eksplicit modellering af **Time Value of Financial Options and Guarantees (TVFOG)**

```
MCEV = Free Surplus
     + Required Capital (med kapitalkostnad)
     + VIF

VIF = Present Value of Future Profits (PVFP)
    − Time Value of Options and Guarantees (TVOG)
    − Cost of Non-Hedgeable Risk (CNHR)
    − Frictional Cost of Capital (FCoC)
```

### 3.2 TVOG – Time Value of Options and Guarantees

For unit-linked med garantier beregnes TVOG via stokastisk modellering:

```
TVOG = E^Q[PV(Garantiomkostning)] − PV(Garantiomkostning ved deterministisk middelscenarie)
```

Beregnes med markedskonsistente scenarier (typisk 1.000-10.000 risiko-neutrale stier).

### 3.3 Unit-linked og MCEV

For ren unit-linked (ingen finansielle garantier) er TVOG typisk **lille eller nul**:
- Ingen rentegaranti → ingen renteoptionstilsvar
- Ingen investeringsgarantier → ingen stokastisk modelleringskrav

Selskabets margin er primært:
- Gebyrer (procent af depot)
- Forsikringsomkostninger (COI margin)
- Administrationsomkostningsmargin

---

## 4. Embedded Value for unit-linked

### 4.1 VIF for unit-linked

For en unit-linked portefølje beregnes VIF som nutidsværdien af:

```
VIF = Σ_t [Gebyrindtægt(t) − Selskabsomkostninger(t)] × DF(t) × Overlevelsessandsynlighed(t)
```

Gebyrindtægt:
```
Gebyr(t) = Forventet_AUM(t) × Gebyrsats
         = D(0) × (1 + r)^t × Gebyrsats
```

### 4.2 Sensitiviteter (operating variances)

Standardiserede sensitiviteter beregnes:

| Stresstest | Effekt på EV/VIF |
|------------|-----------------|
| +1% rente | Typisk positivt (lavere hensættelsesrente) |
| −10% aktier | Reducerer AUM → lavere fremtidige gebyrer |
| +10% omkostninger | Reduktion i VIF |
| −10% dødssandsynligheder | Effekt på COI-margin |

### 4.3 New Business Margin (NBM)

```
NBM = VNB / PVNBP × 100%
```

Hvor PVNBP (Present Value of New Business Premiums) er nutidsværdien af nye præmier.

Typisk NBM for unit-linked produkter: **2-8%** af PVNBP.

---

## 5. EV-rapportering i Danmark

### 5.1 Hvem rapporterer EV?

EV-rapportering er **ikke lovpligtig** i Danmark, men anvendes af:
- Selskaber med internationale moderselskaber (Danica/Danske Bank, SEB Pension, Skandia)
- Selskaber der ønsker at kommunikere underliggende lønnsomhed
- Til intern strategisk planlægning

### 5.2 Danica Pension og EV

Danica Pension rapporterede historisk EV som del af Danske Banks investorkommunikation:
- MCEV-principper
- Separering af unit-linked og garanteret portefølje
- Rapporteret i Danske Banks annual report

### 5.3 Alternativ: Return on Equity og teknik resultat

Mange danske selskaber rapporterer i stedet:
- **Teknisk resultat** (resultat af forsikringsvirksomhed)
- **Investeringsresultat**
- **Afkastgrad**
- **Solvensratio**

---

## 6. Lønnsomhedsanalyse af unit-linked

### 6.1 Produktlønnsomhed

Nøgledrivere for unit-linked lønnsomhed:

```
Profit = Gebyrimtægt − Driftsomkostninger − Forsikringsskader + Erfaringstillæg
       = AUM × Gebyrsats − Faste_omk − Variable_omk − Skade_netto
```

### 6.2 Break-even analyse

Break-even-tidspunkt (politikken er lønsom fra år N):

```
Find N sådan at Σ_{t=0}^{N} PV[Cashflow(t)] = 0
```

For unit-linked produkter: Typisk break-even inden for **3-7 år** afhængig af:
- Erhvervelsesomkostninger
- Gebyrsatser
- Afgangsrate

### 6.3 Lapsetrate (ophørsrate)

Lapse er en central risiko for unit-linked lønnsomhed:

```
Lapse_rate(t) = P(Ophør i år t | Aktiv ved start af år t)
```

Typiske lapseratprofiler:
- År 1-2: Høj lapse (5-15% – kunder fortryder)
- År 3-10: Lav lapse (2-5%)
- År 10+: Meget lav lapse (<2%)

**Lapse-effekt på VIF:**
```
ΔVIF / ΔLAPSE_rate ≈ −PV[fremtidige gebyrer for opphørende policer]
```
