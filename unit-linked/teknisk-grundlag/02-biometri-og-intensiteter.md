# Biometri og Intensiteter i Unit-Linked Forsikring

## 1. Dødelighedsintensiteter

### 1.1 Force of Mortality

**Force of mortality** `μ_x(t)` er den fundamentale biometriske størrelse:

```
μ_x(t) = lim[Δt→0] P(dø i [t, t+Δt] | overlevet til t) / Δt
```

Sammenhæng med overlevelsessandsynlighed:

```
_t p_x = exp(−∫₀ᵗ μ_{x+s} ds)
```

Og til et-årig dødssandsynlighed:

```
q_x = 1 − p_x = 1 − exp(−∫₀¹ μ_{x+s} ds)
```

### 1.2 Makeham-Gompertz-modellen

Den klassiske analytiske model:

```
μ_x = A + B · c^x
```

Parametre:
- **A**: Tilfældig/ekstern dødelighed (konstant)
- **B**: Initial biologisk overlevelsesrate
- **c**: Vækstfaktor (> 1)

Typiske parametre for dansk befolkning (ca. 2010):

| Parameter | Mænd | Kvinder |
|-----------|------|---------|
| A | 0,0006 | 0,0003 |
| B | 0,000056 | 0,000025 |
| c | 1,100 | 1,110 |

### 1.3 Lee-Carter-modellen (generationsdødelighed)

Lee-Carter er standardmodellen for fremtidig dødelighedsprojektion:

```
ln(μ_x(t)) = α_x + β_x · κ_t + ε_x,t
```

Hvor:
- `α_x` = Gennemsnitlig log-dødelighed for alder x
- `β_x` = Alders-specifik følsomhed over for generel trend
- `κ_t` = Tidstrend (periodeindeks)
- `ε_x,t` = Fejlled

**Fremskrivning**: `κ_t` modelleres typisk som random walk with drift:
```
κ_t = κ_{t-1} + d + σ · Z_t
```

Implementeret i Danmark via Finanstilsynets **benchmark-grundlag**.

---

## 2. Benchmark 2014 (BM2014)

### 2.1 Baggrund

Finanstilsynet udgav i 2014 et nyt benchmark-grundlag for levetid (**BM2014**) baseret på:
- Dansk befolkningsstatistik
- Erfaringsdata fra livsforsikringsselskaber
- Lee-Carter-fremskrivning med kohort-korrektioner

### 2.2 Struktur

BM2014 indeholder:
- **Basisintensiteter** `μ_x(2014)` for mænd og kvinder (alder 0-120)
- **Forbedringsfaktorer** `f_x(t)` for fremtidig dødelighedsreduktion

```
μ_x(T) = μ_x(2014) × ∏_{t=2014}^{T} (1 − f_x(t))
```

### 2.3 Kohortbaseret beregning

For en person født i år `Y` der dør/overlever i alder `x` til år `T = Y + x`:

```
Kohort-intensitet: μ_x^Y = μ_x(Y + x)
```

Dvs. personens dødelighed afhænger af BÅDE alder og fødselsår (kohort).

### 2.4 Selskabernes tillæg

Selskaberne tillægger typisk en **sikkerhedsmargin** oven på benchmark:

```
μ_x^selskab = μ_x^BM2014 × (1 − sikkerheds_tillæg)
```

Negativ tillæg = lavere dødelighed = konservativt (selskabet hensætter mere).

---

## 3. Invaliditetsintensiteter

### 3.1 Invaliditetsmodellen

Standard to-tilstands model for invaliditet:

```
Tilstande: Aktiv (A) → Invalid (I) → Død (D)
```

Intensiteter:
- `i_x` = Invaliditetsintensitet (A → I)
- `μ_x^i` = Dødelighedsintensitet for invalider (I → D)
- `μ_x^a` = Dødelighedsintensitet for aktive (A → D)

### 3.2 Erfaringsbaserede intensiteter

Invaliditetsintensiteter varierer med:
- **Alder** (typisk stiger kraftigt fra 45-60 år)
- **Køn** (kvinder har højere invaliditetsrisiko i visse aldersgrupper)
- **Erhvervsgruppe** (manuel vs. kontorarbejde)
- **Konjunktur** (invaliditet stiger i lavkonjunktur)

Typiske kønssplit for invaliditetsintensitet:

| Alder | Mænd (i_x) | Kvinder (i_x) |
|-------|-----------|--------------|
| 30 | 0,0015 | 0,0025 |
| 40 | 0,0040 | 0,0060 |
| 50 | 0,0100 | 0,0150 |
| 60 | 0,0200 | 0,0250 |

*Illustrative tal – de faktiske tal er selskabsspecifikke.*

### 3.3 Reaktiveringsintensitet

I praksis sættes reaktiveringsintensiteten (I → A) typisk til **0** for permanent invaliditet, da de fleste livsforsikringsdækninger definerer permanent invaliditet uden reaktiveringshåb.

---

## 4. Kritisk sygdom (Critical Illness)

### 4.1 Multi-tilstandsmodel

For kritisk sygdom-dækning udvides Markov-modellen:

```
Tilstande: Aktiv → Kritisk syg → Død
                ↓
              Død (fra aktiv)
```

Intensiteter:
- `λ_x` = Incidens for kritisk sygdom (A → CS)
- `μ_x^cs` = Dødelighedsintensitet efter kritisk sygdom (CS → D)
- `μ_x^a` = Baggrundsmortalitet for aktive (A → D)

### 4.2 CI-sygdomme

Typiske dækninger i dansk praksis:
- Kræft (alle typer)
- Hjerteanfald (AMI)
- Apopleksi (stroke)
- Kronisk nyresvigt
- Multipel sklerose
- Visse hjerteoperationer

---

## 5. Ægtefælle- og børnedækninger

### 5.1 Fælles overlevelsessandsynlighed

For ægtefælledækning (livrente til efterlevende):

```
_t p_{xy} = _t p_x × _t p_y   [ved uafhængig dødelighed]
```

Rentesandsynlighed for fælles livrente:
```
_t p_{xy}^{ij} = P(begge overlever t) = _t p_x × _t p_y
```

### 5.2 Afhængig dødelighed (broken heart syndrome)

I virkeligheden er ægtefællers dødsfald IKKE uafhængige:
- Øget dødelighedsrisiko for den efterlevende ægtefælle i de første år
- Modelleres via **copula-modeller** eller **shared frailty**

For standard beregninger antages typisk **uafhængighed**.

---

## 6. Stokastiske dødelighedsmodeller

### 6.1 Cairns-Blake-Dowd (CBD) modellen

Alternativ til Lee-Carter, velegnet til ældre aldersgrupper:

```
logit(q_x(t)) = κ_t^(1) + κ_t^(2) × (x − x̄)
```

Parametre:
- `κ_t^(1)`: Generelt dødelighedsniveau (random walk)
- `κ_t^(2)`: Hældning (alderseffekt)

### 6.2 Stokastisk levetidsrisiko i Solvens II

Under Solvens II's standard formula:

**Levetidsrisiko-stress:**
```
SCR_longevity = ΔBELLiability under 20% reduktion i dødelighedsintensiteter
```

Dvs. hvis alle forsikrede lever 20% længere end antaget, hvad er ΔBELiabilities?

**Dødelighedsrisiko-stress:**
```
SCR_mortality = ΔBELLiability under 15% stigning i dødelighedsintensiteter
```

### 6.3 Kapitaleffekt for unit-linked

For ren unit-linked (ingen garantier, ingen livrente) er biometri-kapitalkravet lavt:
- Levetidsrisiko: Minimal (ingen livrente → ingen udbetalingsforpligtelse udover depot)
- Dødelighedsrisiko: Moderat (risikosummer finansieret via COI, men fejlestimat af COI)
- Invaliditetsrisiko: Afhænger af dækningens størrelse

---

## 7. Datakilder for biometri i Danmark

| Kilde | Indhold | Tilgængelighed |
|-------|---------|----------------|
| **Danmarks Statistik** | Befolkningsdødelighed, befolkningsregister | Offentlig |
| **Finanstilsynet (BM2014)** | Branche-benchmark dødelighedstabeller | Offentlig (Finanstilsynets hjemmeside) |
| **Forsikring & Pension** | Branche-erfaringsdata (aggregeret) | Branche-intern |
| **SCOR / RGA / Munich Re** | Genforsikrer-statistikker | Kontraktuel |
| **CPR-registret** | Individuelle CPR-data (til eget erfaringsgrundlag) | Forsikringsselskaber via lov |
| **Sygehusregistret** | Invaliditets- og sygdomsdata | Forsikringsselskaber via lov |
