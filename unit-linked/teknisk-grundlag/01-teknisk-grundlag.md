# Teknisk Grundlag for Unit-Linked Forsikring i Danmark

## 1. Hvad er teknisk grundlag?

**Teknisk grundlag** er det sæt af aktuarmæssige og finansielle forudsætninger, som et forsikringsselskab anvender til beregning af:

- Forsikringspræmier
- Forsikringsmæssige hensættelser
- Fripoliceværdier og kontantværdier
- Bonusgrundlag (for produkter med bonus)

For unit-linked produkter er teknisk grundlag mere begrænset end for traditionelle garanterede produkter, men biometrien er stadig central.

---

## 2. Biometriske grundlag

### 2.1 Dødelighedsintensiteter

**Dødelighedsintensitet** `μ_x(t)` (også kaldet force of mortality) angiver den øjeblikkelige sandsynlighed for at dø for en person af alder x:

```
q_x ≈ 1 − exp(−∫μ_x(s)ds)   [for et-årsintervaller]
```

#### Officielle grundlag i Danmark

**G82-tabeller (Grundlag 1982)**
- Historisk standardgrundlag for danske livsforsikringsselskaber
- Separate tabeller for mænd (G82M) og kvinder (G82K)
- Baseret på dansk befolkningsdødelighed 1982
- Konservative (høj overlevelse = højere hensættelser)

**GP93 og G82 med tillæg**
- Opdaterede grundlag fra 1990'erne
- Tillæg for forventet fremtidig levetidsforbedring

**Nuværende praksis (fra ca. 2010)**
- De fleste selskaber anvender **individuelle selskabsspecifikke grundlag**
- Baseret på eget erfaringsgrundlag + population data
- Tillæg for **kohort-effekter** (levetidsforbedring over generationer)

### 2.2 Benchmark grundlag

Finanstilsynet anbefaler brug af branchebaserede grundlag:

**Benchmark 2014 / BM2014:**
- Udgivet af Finanstilsynet
- Køns- og aldersdifferentierede intensiteter
- Inkorporerer fremtidig levetidsforbedring
- Generationsbaserede tabeller (kohortprojektioner)

### 2.3 Levetidsforbedring (mortality improvement)

Fremtidig levetidsforbedring modelleres typisk som:

```
μ_x(t + s) = μ_x(t) × exp(−λ_x × s)
```

Hvor `λ_x` er forbedringsfaktoren for alder x. Alternativt bruges **Lee-Carter modellen**:

```
ln(μ_x(t)) = α_x + β_x × κ_t
```

Og `κ_t` fremregnes stokastisk (typisk med en random walk with drift).

### 2.4 Invaliditetsintensiteter

Invaliditetsintensitet `i_x` angiver sandsynlighed for at overgå fra aktiv til invalid:

```
i_x = Antal nye invalider alder x / Eksponering alder x
```

Baseret på:
- Selskabets eget erfaringsdata
- Branchedata fra Forsikring & Pension
- Arbejdsmarkedsbaserede data

---

## 3. Rentegrundlag

### 3.1 Beregningsrente for hensættelser

Ifølge Solvens II beregnes hensættelser med **risikofri rente** (EIOPA's risikofrirente-kurve):

```
Bedste skøn (Best Estimate Liabilities) = Σ[CF(t) × DF(t)]
```

Hvor `DF(t)` er diskonteringsfaktoren baseret på EIOPA's rentekurve:

```
DF(t) = 1 / (1 + r_f(t))^t
```

EIOPA's rente for EUR og DKK publiceres månedligt og inkluderer:
- Swapkurve (swaprenter)
- Volatilitetsækvivalent (VA – Volatility Adjustment)
- Matching Adjustment (for godkendte selskaber)
- Ultimativt forventet afkast (UFR – Ultimate Forward Rate)

### 3.2 Historiske beregningsrenter

| Periode | Beregningsrente (traditionel) |
|---------|-------------------------------|
| Før 1994 | 4,5% p.a. |
| 1994-1999 | 2,5% p.a. |
| 1999-2006 | 3,0% → 2,5% |
| 2006-2011 | Markedsbaseret kurve introduceres |
| 2016- | EIOPA rentekurve (Solvens II) |

For **unit-linked** er den garanterede beregningsrente typisk 0% (ingen rentegaranti).

### 3.3 UFR (Ultimate Forward Rate)

EIOPA's UFR er sat til **3,45%** (per 2024) for EUR/DKK:

- Anvendes som langsigtet forwardrente for løbetider > LLP (Last Liquid Point)
- For DKK er LLP typisk 20 år
- Konvergerer fra observeret kurve til UFR over 40 år

---

## 4. Omkostningsgrundlag

### 4.1 Omkostningstyper i teknisk grundlag

```
Totale omkostninger = Erhvervelsesomkostninger + Administrationsomkostninger
                    + Skadebehandlingsomkostninger + Investeringsomkostninger
```

**Erhvervelsesomkostninger:**
- Provision til sælgere/rådgivere
- Tegningsomkostninger
- Afskrives over policeperioden

**Administrationsomkostninger:**
- Fast beløb pr. police pr. år
- Procent af depotstørrelse
- Procent af præmie

### 4.2 ÅOP (Årlige Omkostninger i Procent)

ÅOP er et standardiseret mål for de samlede omkostninger, der skal oplyses til kunder:

```
ÅOP = r_brutto − r_netto
```

Beregnes som forskellen mellem det interne afkast uden og med omkostninger, ekskl. forsikringsomkostninger.

**Typiske ÅOP-niveauer (2024):**
| Segment | ÅOP-interval |
|---------|--------------|
| Store firmapensioner | 0,3 – 0,7% |
| Individuelle pensioner | 0,7 – 1,5% |
| Indbetalingsstopper | 0,5 – 1,0% |

---

## 5. Risikogrundlag vs. erfaringsgrundlag

### 5.1 Risikogrundlag (beregningsgrundlag)

Bruges til præmieberegning og hensættelser:
- **Konservativt**: Indeholder sikkerheds-margins
- Overvurderer risiko → bygger bonuspotentiale op

### 5.2 Erfaringsgrundlag (forventningsgrundlag / best estimate)

Bruges til bedste skøn (Best Estimate Liabilities under Solvens II):
- **Realistisk**: Bedst mulige skøn
- Baseret på historiske erfaringsdata
- Opdateres løbende

### 5.3 Risikomar­gin

Under Solvens II skal der tillægges en **risikomargin** til Best Estimate:

```
RM = CoC × Σ[SCR_t / (1 + r_f(t))^t]
```

Hvor:
- `CoC` = Cost-of-Capital sats (6% jf. Solvens II)
- `SCR_t` = Forventet SCR for ikke-afsikringsbare risici på tidspunkt t

---

## 6. Selskabsspecifikke parametre

### 6.1 PFA's tekniske grundlag

PFA anvender eget aktuargrundlag baseret på:
- Intern statistik over +700.000 forsikrede
- Ajourføres ved aktuarmæssig statusopgørelse
- Generationsbaseret dødelighedsprojektion
- Selskabsspecifikt invaliditetsgrundlag

### 6.2 Danica Pension

Danica anvender:
- Branchebaserede grundlag som benchmark
- Interne erfaringsdata som supplement
- Robusthedstest ved afvigelse fra branchegennemsnit

### 6.3 Velliv

Velliv anvender eget aktuargrundlag med:
- Opdaterede dødelighedstabeller baseret på historik fra Nordea Liv & Pension (nu Velliv)
- Separate grundlag for arbejdsdygtighedsrisici

---

## 7. Valideringsproces

### 7.1 Aktuar-ansvar

Den ansvarshavende aktuar (AA) skal:
1. Sikre at teknisk grundlag er tilstrækkeligt
2. Underskrive aktuarerklæringen i årsrapport
3. Rapportere til bestyrelse og Finanstilsynet

### 7.2 Tilstrækkelighed og stress

Finanstilsynet kræver regelmæssige stresstests:
- **Dødelighedsstress**: +20% / -20% i dødelighedsintensiteter
- **Levetidsstress**: Permanent stigning i overlevelsessandsynligheder
- **Invaliditetsstress**: +35% i invaliditetsintensiteter

### 7.3 Aktuarmæssig statusopgørelse

Hvert år gennemføres aktuarmæssig statusopgørelse:
- Sammenligner faktiske erfaringer med teknisk grundlag
- Estimerer erfaringstillæg (bonus/modregning)
- Revideres af ekstern revisor
