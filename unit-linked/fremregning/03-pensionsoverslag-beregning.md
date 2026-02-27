# Pensionsoverslag – Detaljeret Beregningsmetodik

## 1. Lovgrundlag og formål

Pensionsoverslag er lovpligtig information til forsikringstagere om forventet pension. Reglerne fremgår af:

- **Bekendtgørelse om god skik** (god skik-bekendtgørelsen)
- **Pensionsoverslagsbekendtgørelsen**
- **Vejledning fra Forsikring & Pension** om afkastforudsætninger

Formål:
1. Forsikringstager kan planlægge sin pensionsøkonomi
2. Sikre sammenlignelighed på tværs af selskaber
3. Fremme gennemsigtighed om omkostninger

---

## 2. Input til pensionsoverslag

### 2.1 Forsikringsspecifikke data

```
Nuværende depot:         D(0)
Månedlig præmie:         P
Pensionsalder:           T_P (typisk folkepensionsalder + 0-5 år)
Nuværende alder:         x
Køn:                     M/K
Investeringsprofil:      Profil (risiko/aktivallokering)
```

### 2.2 Afkastforudsætninger (Forsikring & Pension 2024 – vejledende)

Eksempel på typisk vejledende struktur:

| Aktivklasse | Lav (realafkast) | Middel (realafkast) | Høj (realafkast) |
|-------------|-----------------|--------------------|--------------------|
| Globale aktier | −1% | 3,5% | 8% |
| Obligationer (stats) | −1% | 0% | 2% |
| Kreditobligationer | −0,5% | 1% | 3% |
| Ejendom | 0% | 2% | 5% |
| Inflationsforudsætning | | 2% | |

*Nominelt afkast = Realafkast + Inflation*

### 2.3 Omkostningsforudsætninger

```
ÅOP = Administrations-ÅOP + Investerings-ÅOP
    = (Fast gebyr + Depotgebyr) / Depot + Investeringsomkostninger
```

---

## 3. Fremregning trin-for-trin

### 3.1 Månedlig depotfremregning

```python
# Pseudo-kode for månedlig fremregning

depot = D_start
for maaned in range(1, N_maaneder + 1):
    alder = x + maaned / 12

    # Månedlig afkastrate
    r_maaned = (1 + r_aarslig) ** (1/12) - 1

    # Tilskriv afkast
    depot = depot * (1 + r_maaned)

    # Tilskriv præmie (efter præmiegebyr)
    praemie_netto = P * (1 - praemiegebyr_pct)
    depot += praemie_netto

    # Fradrag: forsikringsomkostning (COI)
    risikosum = max(0, forsikringssum - depot)
    coi = risikosum * q_x_maanedlig(alder, koen)
    depot -= coi

    # Fradrag: depotgebyr
    depot -= depot * (depotgebyr_pct / 12)

    # PAL-acontobetaling (kvartalsvis)
    if maaned % 3 == 0:
        pal = beregn_pal_acontobetaling(depot, foregaaende_depot)
        depot -= pal
```

### 3.2 Tre-scenarie fremregning

For hvert af de tre scenarier (lav/middel/høj):

```
D_lav(T)    = fremregn(D_0, r_lav, P, T)
D_middel(T) = fremregn(D_0, r_middel, P, T)
D_hoej(T)   = fremregn(D_0, r_hoej, P, T)
```

### 3.3 Konvertering til månedlig pension

**Livsvarig livrente (uden garanti):**

```
Månedlig pension = D(T) / a_x(T, r_rente)
```

Annuitetsfaktor `a_x` beregnes ud fra:
- Alder x ved pensionering
- Køn
- Aktuarielle dødelighedstabeller (fx BM2014)
- Diskonteringsrente r (fx 0-2% p.a.)

**Ratepension (10 år):**

```
Månedlig rate_år1 = D(T) / 120   [simpel]
```

Herefter varierer raten med afkastet (for unit-linked ratepension).

---

## 4. Håndtering af livscyklus i fremregning

### 4.1 Aldersjusteret allokering

For produkter med automatisk livscyklus ændres aktivallokeringen over tid:

```
Allokering(alder) = f(Profil, alder, pensionsalder)
```

Eksempel (PFA C-profil med livscyklus):

| Alder | Aktier | Obligationer | Andet |
|-------|--------|-------------|-------|
| 25 | 80% | 15% | 5% |
| 35 | 75% | 20% | 5% |
| 45 | 60% | 35% | 5% |
| 55 | 45% | 50% | 5% |
| 65 | 25% | 70% | 5% |

For hvert år opdateres forventet afkast baseret på aktuel allokering:

```
r_forventet(alder) = Σ [w_i(alder) × r_i]
```

### 4.2 Afkastens standardafvigelse over tid

For stokastiske overslag:
```
σ_portefølje(alder) = √[Σ_i Σ_j w_i × w_j × σ_i × σ_j × ρ_ij]
```

---

## 5. Pensionsinfo-integration

### 5.1 PensionsInfo dataudveksling

**PensionsInfo** er den fælles digitale platform, der aggregerer pensionsdata fra alle udbydere.

Datastruktur sendt til PensionsInfo:

```xml
<Pension>
  <Ident>forsikringstagers_CPR_nummer</Ident>
  <Produkt>Ratepension (markedsrente)</Produkt>
  <DepotværdiIDag>500000</DepotværdiIDag>
  <MånedligPræmie>3000</MånedligPræmie>
  <ForventetPensionMånedlig>
    <Lav>8500</Lav>
    <Middel>14000</Middel>
    <Høj>22000</Høj>
  </ForventetPensionMånedlig>
  <Dækning>
    <Invaliditet>25000</Invaliditet>
    <DødsfaldSum>500000</DødsfaldSum>
  </Dækning>
</Pension>
```

### 5.2 Samlet pensionsoversigt

PensionsInfo aggregerer overslag fra alle selskaber og viser en samlet oversigt inkl. folkepension.

---

## 6. Fripolice-fremregning

### 6.1 Hvad er fripolice?

Fripolice opstår når forsikringstager ophører med præmieindbetaling, men lader forsikringen løbe videre.

### 6.2 Fripoliceberegning for unit-linked

For unit-linked er fripoliceberegning enkel:

```
Fripoliceværdi = Nuværende depotværdi
```

Depotet fortsætter med at være investeret, og forsikringsomkostninger (COI) trækkes løbende fra depotet.

**Fripolice-dækning** reduceres typisk proportionalt:

```
Fripolice_forsikringssum = Aktuel_sum × (Fripoliceværdi / TP_fuld_præmiebetaling)
```

### 6.3 Fripolice-fremregning til pensioneringstidspunkt

```
D_fripolice(T) = D_fripolice(0) × ∏(1 + r_netto(t)) − Σ COI(t)
```

Fremregnes med de samme scenarieantagelser som for aktive policer.

---

## 7. Kontantværdi

### 7.1 Kontantværdi (tilbagekøb)

Kontantværdien er det beløb forsikringstager modtager ved tilbagekøb:

```
Kontantværdi = Depotværdi − Tilbagekøbsfradrag
```

For moderne unit-linked produkter: **Tilbagekøbsfradrag = 0 kr.**

Skattemæssigt (pensionsordning):
```
Netto_kontantværdi = Kontantværdi − 60% beskatning (ved tidligt ophæv)
```

### 7.2 Tilbagekøbsfradrag (historisk)

Ældre forsikringspolicer kan have tilbagekøbsfradrag:

| Forsikringens alder | Fradragsats |
|---------------------|-------------|
| < 1 år | 15% |
| 1-3 år | 10% |
| 3-5 år | 5% |
| > 5 år | 0% |

---

## 8. Følsomhedsanalyse for pensionsoverslag

### 8.1 Afkastfølsomhed (typiske resultater)

For en 35-årig med 100.000 kr. depot og 3.000 kr./måned i præmie (30 år til pension):

| Afkast (netto) | Depot ved pension | Månedlig livrente (ca.) |
|----------------|-----------------|------------------------|
| 1% p.a. | ~1,5 mio. | ~5.500 kr./md. |
| 3% p.a. | ~2,2 mio. | ~8.000 kr./md. |
| 5% p.a. | ~3,3 mio. | ~12.000 kr./md. |
| 7% p.a. | ~4,9 mio. | ~18.000 kr./md. |

*Beregnet med Benchmark 2014-dødelighedstabeller, rente = 0% ved konvertering.*

### 8.2 Tidsfølsomhed

Effekten af at starte 10 år tidligere (25 vs. 35 år ved start, ellers ens):

```
Ratio depot(25 år start) / depot(35 år start) ≈ (1 + r)^10 ≈ 1,8 ved 6% afkast
```

Dvs. 10 års ekstra opsparing giver ca. 80% mere depot.
