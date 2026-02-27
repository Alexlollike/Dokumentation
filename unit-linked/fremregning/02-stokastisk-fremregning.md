# Stokastisk Fremregning af Unit-Linked Policer

## 1. Motivation for stokastisk modellering

Deterministiske fremregninger med faste scenarier giver ikke et fuldstændigt billede af risikoen i en unit-linked police. Stokastiske modeller anvendes til:

- **Solvens II SCR-beregning** – stresstest og risikokapital
- **Embedded Value** – MCEV/EV beregninger
- **Produktdesign** – vurdering af optioner og garantier
- **Intern risikostyring** – ORSA (Own Risk and Solvency Assessment)

---

## 2. Afkastmodeller

### 2.1 Geometrisk Brownsk Bevægelse (GBM)

Den klassiske model for aktieafkast:

```
dS(t) = μ · S(t) · dt + σ · S(t) · dW(t)
```

Diskretiseret:
```
S(t+Δt) = S(t) · exp((μ - σ²/2) · Δt + σ · √Δt · Z)
```

Hvor:
- `μ` = Forventet afkast (drift)
- `σ` = Volatilitet
- `Z` ~ N(0,1) = Standard normalfordelt stokastisk variabel
- `W(t)` = Wiener-proces (Brownsk bevægelse)

**Parametre (illustrative):**
| Aktivklasse | μ (p.a.) | σ (p.a.) |
|-------------|-----------|-----------|
| Globale aktier | 7% | 15-20% |
| Europæiske aktier | 6-7% | 16-22% |
| Obligationer (lang) | 2-3% | 6-8% |
| Kreditobligationer | 3-4% | 5-8% |

### 2.2 Stochastic Volatility (Heston-model)

```
dS(t) = μ · S(t) · dt + √v(t) · S(t) · dW_S(t)
dv(t) = κ(θ − v(t)) · dt + ξ · √v(t) · dW_v(t)
```

Hvor:
- `v(t)` = Stokastisk varians
- `κ` = Mean-reversion hastighed
- `θ` = Langsigtet variansgennemsnit
- `ξ` = Volatilitet-af-volatilitet
- `corr(dW_S, dW_v) = ρ` (typisk negativ korrelation)

### 2.3 Rentemodeller

**Vasicek-model:**
```
dr(t) = κ(θ − r(t)) · dt + σ · dW(t)
```

**Hull-White (extended Vasicek):**
```
dr(t) = (θ(t) − κ · r(t)) · dt + σ · dW(t)
```

Bruges til at modellere renten, der påvirker:
- Obligationsafkast
- Konversionsfaktor ved pensionering
- Diskonteringsrente for hensættelser

### 2.4 Multi-faktor og regime-switching modeller

Mere avancerede modeller inkorporerer:
- **Regime-switching**: Markedet veksler mellem "normal" og "krise" regimer
- **Jump-diffusion**: Pludselige spring i aktivpriser (Merton-model)
- **Multi-faktor**: Flere uafhængige risikofaktorer

---

## 3. Monte Carlo-simulering

### 3.1 Fremgangsmåde

```
For n = 1 til N:          # N simulationsscenarier (typisk 1.000 – 100.000)
    Simulér afkaststi r_n(1), r_n(2), ..., r_n(T)
    Beregn depotsti D_n(0), D_n(1), ..., D_n(T)
    Beregn cashflows CF_n(t) for hvert tidspunkt
    Beregn nutidsværdi: NPV_n = Σ[CF_n(t) × DF(t)]
Aggregér: E[NPV] = Σ NPV_n / N
```

### 3.2 Variansreduktion

For at forbedre simulationseffektiviteten:

- **Antitetiske variable**: Kør simulationer i par (+Z og -Z)
- **Kontrol-variablen**: Brug analytisk beregning til at reducere variansen
- **Stratificeret sampling**: Opdel simulationsrummet systematisk
- **Quasi-Monte Carlo**: Brug Sobol- eller Halton-sekvenser i stedet for pseudotilfældige tal

### 3.3 Scenario-generation (ESG)

**Economic Scenario Generators (ESG)** genererer konsistente, markedskonsistente scenarier på tværs af aktivklasser. Brugt til:

- Solvens II interne modeller
- MCEV/EV beregninger
- ALM simuleringer

Krav til markedskonsistente ESG:
- Arbitrage-fri prissætning
- Kalibreret til observerede markedspriser
- Konsistent med risikoneutrale sandsynligheder (Q-mål)

---

## 4. Policeniveaumodellering

### 4.1 Stadie-baseret model (Markov-kæde)

Forsikringstagerens livsløb modelleres som en Markov-kæde med tilstande:

```
Tilstande: {Aktiv, Invalid, Død, Pensioneret, Fripolice}
```

Overgangsintensiteter:
- `μ_ad` = Aktiv → Død (dødelighedsintensitet)
- `μ_ai` = Aktiv → Invalid (invaliditetsintensitet)
- `μ_id` = Invalid → Død (dødelighedsintensitet for invalider)
- `μ_ia` = Invalid → Aktiv (reaktiveringsintensitet, typisk 0)

### 4.2 Koblede differential-ligninger (Kolmogorov-ligninger)

For overgangsandele `p_ij(t, T)`:

```
d/dt p_aa(t, T) = −[μ_ad(t) + μ_ai(t)] · p_aa(t, T)
```

```
d/dt p_ai(t, T) = μ_ai(t) · p_aa(t, T) − μ_id(t) · p_ai(t, T)
```

### 4.3 Cashflow-projektion

For hvert tidspunkt `t` og tilstandsovergang:

```
CF(t) = p_aa(t) · [P(t) − C_adm(t) − COI(t)]
      + p_ad(t) · B_død         # Dødsfaldsudbetaling
      + p_ai(t) · B_invalid(t)  # Invaliditetsudbetaling
      + p_aR(t) · B_pension(t)  # Pensionsudbetaling
```

---

## 5. Sensitivitetsanalyser

### 5.1 Investeringsafkast

Sensitivitet over for afkastforudsætningen:

```
ΔD(T) / Δr ≈ T × D(T) / (1 + r)   [første-ordens approksimation]
```

For et depot på 1 mio. kr., 30 år til pension og 6% forventet afkast:
- +1% afkast → ca. +30% større depot
- -1% afkast → ca. -23% mindre depot

### 5.2 Dødelighedsforudsætninger

Sensitivitet over for levetidsforudsætning (`K90`, `G82` mv.):

- **Langt liv**: Kræver større hensættelser for livrente
- **Kort liv**: Lavere hensættelse, men risiko for utilstrækkelige reserver

### 5.3 Omkostningssensitivitet

ÅOP-effekt over 30 år:

| ÅOP | Depotindeks (basis=0%) |
|-----|------------------------|
| 0,0% | 100 |
| 0,5% | ~86 |
| 1,0% | ~74 |
| 1,5% | ~64 |
| 2,0% | ~55 |

*Beregnet ved 6% bruttoafkast over 30 år.*

---

## 6. ORSA og internt kapitalkrav

### 6.1 ORSA-fremregning (Solvens II)

Under **ORSA (Own Risk and Solvency Assessment)** fremregnes selskabets samlede solvens over en flerårig horisont (typisk 3-5 år):

- SCR (Solvency Capital Requirement) fremregnes
- Egentlige kapitalgrundlag (Own Funds) fremregnes
- Solvensratio = Own Funds / SCR holdes over 100%

### 6.2 Reverse stress testing

Find det scenarie, der netop fører til insolvens:

```
Find r* sådan at: Own Funds(r*) / SCR(r*) = 1
```

---

## 7. Softwareværktøjer til fremregning

| Softwareplatform | Anvendelse | Brugt af |
|-----------------|------------|---------|
| **Prophet (FIS)** | Aktuarmæssig modellering | Danica, Nordea, Topdanmark |
| **MoSes (Milliman)** | Aktuarmæssig modellering | Skandia, SEB |
| **R (aktuar-pakker)** | Ad-hoc fremregning, analyse | Intern analyse |
| **Python (scipy, numpy)** | Tilpassede modeller | Interne teams |
| **Axis (Willis Towers Watson)** | Stokastisk modellering | Konsulentbrug |
| **Excel + VBA** | Enklere fremregninger | Alle selskaber |

Prophet og MoSes er branchestandarder for deterministiske og stokastiske livsforsikringsberegninger i Danmark og internationalt.
