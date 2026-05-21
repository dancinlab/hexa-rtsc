<!-- @created: 2026-05-12 -->
<!-- @scope: real-limits audit (Wave M) — room-temperature superconductor candidate + 48 T SC coil substrate -->
<!-- @authority: applies LATTICE_POLICY.md §1.2 taxonomy verbatim -->
---
type: limit-breakthrough-audit
wave: M
session: 2026-05-12
parent_policy: LATTICE_POLICY.md §1.2
applies_to: hexa-rtsc — Room-Temp Superconductor + 48 T SC coil substrate-of-substrates
---

# LIMIT_BREAKTHROUGH.md — hexa-rtsc real-limits audit (Wave M)

> **Question**: hexa-rtsc claims a Tc = 300 K, Hc2 = 48 T closed-form
> candidate spec. RT-SC is **academically unproven** (claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) et al.
> not replicated). What are the **physics walls** the candidate must
> clear, and which can be broken vs. which are HARD?

---

## §1 Domain identification

| Layer | Verbs | Concern |
|-------|-------|---------|
| RTSC | `rtsc/` — Tc = 300 K, Hc2 = 48 T, Cooper-pair φ = 2 | Room-temp superconductor candidate spec |
| SC | `sc/` — BCS, Abrikosov vortex CN = 6 | Established low-T superconductor lineage |
| Falsifier preregister | F-RTSC-{1,2,3} + F-SC-{1,2,3} | 6 falsifier register, archival closure |
| Firmware | `firmware/` (70/70 sim + HDL + MCU) | Coil-driver + Meissner-test bench scaffolds |
| Substrate consumers | hexa-fusion (48 T coil), hexa-ufo (Meissner levitation), hexa-cern (accel magnet) | Downstream dependency map |

v1.1.0 is "RSC code-layer FINAL" — book-keeping closure, **not
empirical validation**. The audit treats the candidate spec as
what's actually under test against physics walls.

---

## §2 Real limits applicable to hexa-rtsc

### 2.1 BCS coupling-strength → Tc ceiling (PHYSICAL)

BCS: Tc ∝ ω_D · exp(−1 / (N(0) · V)). For phonon-mediated mechanism,
ω_D (Debye frequency) caps Tc at ~30-40 K in conventional metals.
**~150 K (hydride family) was the experimental record under
pressure** (LaH₁₀, CSH at >200 GPa). At ambient pressure, the
highest confirmed Tc is ~138 K (Hg-Ba-Ca-Cu-O class cuprate).

A 300 K Tc at ambient *requires* a non-phonon mechanism or extreme
electron-phonon coupling outside the BCS regime.

### 2.2 Hc2 critical-field ceiling (PHYSICAL)

```
H_c2(0)  ≈  (Φ_0) / (2π · ξ²)        (Ginzburg-Landau)
H_c2(0)  ≤  H_Pauli  =  1.86 · Tc · (k_B / μ_B)   (Pauli limit, singlet)
```

Pauli paramagnetic limit at Tc = 300 K: ~560 T. **48 T is well
below this** — *not* a fundamental wall. Existing Nb₃Sn / REBCO at
helium reach 25-30 T routinely; 48 T at 300 K is "only" a 2× ratio
over current best HTS at LN₂.

### 2.3 Replication / falsification under PAC sample bound (MATHEMATICAL)

claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) (2023) was claimed and then **failed to replicate** across
~12+ independent labs in ~6 months. For a positive RT-SC claim to
be accepted, **PAC-style independent replications** at ε=0.05, δ=0.01
typically demand ≥ 5-7 independent groups with full materials chain
disclosure. **No room-temp claim has cleared this bar to date.**

### 2.4 Carnot ceiling DOES NOT bind (PHYSICAL)

Superconductor is **not** a heat engine — Cooper-pair condensate
carries current with zero resistance, no thermodynamic-cycle ceiling.
Carnot is irrelevant. Cited only to clarify what *isn't* a wall.

### 2.5 Materials-discovery throughput (ENGINEERING)

High-throughput materials synthesis (e.g., CALYPSO, USPEX-style ab
initio + experimental MPW combinatorial) screens ~10³-10⁴ candidate
stoichiometries / month per lab. Total chemical space of plausible
RT-SC candidates ≈ 10⁷ (binary + ternary + quaternary intermetallics
with light + heavy atom mixes). **At current cadence, exhaustive
screening would take ~10³ lab-years.**

### 2.6 ML / surrogate-discovery acceleration (ENGINEERING)

DFT + ML surrogates (e.g., Megnet, M3GNet, MACE) accelerate
candidate-screening by ~100-1000×. Combined with focused-synthesis
loops, ~10⁴ candidates/month becomes ~10⁶/month. **Still ~10
lab-years for exhaustive sweep** — but reachable.

### 2.7 Cryogenic-coil baseline (ENGINEERING)

Even without RT-SC, REBCO + Nb₃Sn + LTS coils at 20 K (high-Tc
conduction-cooled) reach **30-40 T** today (NHMFL Tallahassee,
MIT-PSFC SPARC). A 48 T cryogenic coil is feasible *now* without
RT-SC. RT-SC's value is **eliminating the cryocooler stack**, not
exceeding 48 T.

### 2.8 Statistical power on "Meissner effect observed" (MATHEMATICAL)

Meissner-flux-expulsion measurements are confounded by ferromagnetic
impurities (claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) lesson). To distinguish bulk Meissner from
spurious diamagnetism at e.g., volume fraction f = 1%, need
SQUID-magnetometry with SNR > 40 dB **and** independent calorimetric
Tc transition + zero-resistance + flux-pinning lattice imaging. Each
of the 4 measurements has independent false-positive risk ~10⁻²;
joint requirement → false-positive ~10⁻⁸. **Sufficient for honest
claim.**

---

## §3 Per-limit breakthrough assessment

### 3.1 BCS Tc ceiling at ambient → **UNCLEAR**

Conventional BCS at ambient pressure caps ~40 K. Cuprates (138 K)
already exceed BCS via non-phonon (likely spin-fluctuation) pairing
— mechanism still debated. A genuine 300 K ambient RT-SC requires a
**new pairing mechanism** (or extreme combination of d-wave / topological
/ polaronic) that is **physically conceivable but empirically unverified**.

**Trigger** (positive): an independently-replicated material with
Tc > 200 K at ambient passing the §2.8 4-measurement gate. Status:
**not achieved at time of writing**.

**Trigger** (negative): exhaustive ML+experimental sweep of binary
+ ternary intermetallics (§2.5/2.6) returning no candidate → strong
empirical evidence ambient 300 K is inaccessible.

### 3.2 Hc2 = 48 T → **BREAKABLE_WITH_TECH**

Not a wall in fundamental physics (Pauli limit at 300 K ≈ 560 T).
Achievable with REBCO at 20 K *today*; just expensive cryogenically.
RT-SC would deliver it without the cryo penalty. **The number 48 T
is engineering-conservative**, not physics-binding.

### 3.3 PAC replication bound → **HARD_WALL on claim acceptance** (procedural)

A single lab's claim is **never** sufficient for RT-SC acceptance,
by community norm (post-Schön, post-claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim)). 5-7 independent
replications with full materials disclosure is the binding bar.

**Trigger**: replication consortium publishing parallel synthesis
campaigns with shared material lots. Status: emerging post-claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) era
but no consortium yet active.

### 3.4 Carnot irrelevance → **N/A (catalog)**

Not a wall here.

### 3.5 Materials-discovery throughput → **BREAKABLE_WITH_TECH**

ML+robotics labs (e.g., A-Lab @ LBNL 2023, Toyota-MIT, DeepMind GNoME)
scale to 10⁴-10⁵ inorganic candidates per year per lab. Trigger:
ML-driven *closed-loop* RT-SC search with weekly synthesis batches.
Already running at A-Lab tier; specific RT-SC focus is plausible
within 3-5 years.

### 3.6 ML surrogate acceleration → **BREAKABLE_WITH_TECH**

Pure engineering. Current state of the art (MACE, Allegro) → ~1k×
DFT speedup with maintained accuracy on intermetallic energies.
Trigger: published "RT-SC scouting" benchmark + leaderboard.

### 3.7 Cryogenic-coil baseline → **BREAKABLE_WITH_TECH** (already broken at 30-40 T)

48 T at 20 K is a 2-3 yr engineering reach for a well-funded program.
No new physics. **hexa-rtsc's 48 T target is achievable without
RT-SC** — important honest framing: RT-SC is about *cost* (no cryo),
not *peak field*.

### 3.8 Statistical-power gate → **HARD_WALL** (procedural)

The 4-independent-measurement gate (resistivity zero + Meissner +
specific-heat anomaly + flux-line lattice) is community-binding.
Each is necessary; together sufficient. **Cannot be skipped.**
Mitigation: design experiments to clear *all four* on the same
sample lot.

---

## §4 Top-3 breakthrough opportunities

### #1 — ML-driven closed-loop RT-SC search (§3.5 + §3.6)

The single largest tractable lever. Combines materials-discovery
throughput (~10⁵ candidates/yr) with surrogate-pruned synthesis
batches. Even a *negative* outcome (no RT-SC candidate found in
binary + ternary intermetallics) is publication-worthy and tightens
the physics floor. Time: 3-5 yr to first systematic sweep.

### #2 — Replication consortium founding (§3.3)

Post-claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) community is primed; an RT-SC replication consortium
with shared materials lots + parallel synthesis would convert "claim"
to "accepted" in ~6-12 months *if a real candidate emerges*. Trigger
is institutional, not technical. ~0 capex, high payoff.

### #3 — 48 T REBCO coil for hexa-fusion / hexa-cern *without* RT-SC (§3.7)

Honest fallback: the substrate-consumer applications (fusion confinement,
accelerator beamline) **don't require RT-SC** — they require 48 T
**at any temperature with practical cryogenics**. Funding a REBCO
+ Bi-2212 hybrid coil program decouples hexa-rtsc downstream success
from the academically-unproven RT-SC claim.

---

## §5 Honest caveats

1. **RT-SC IS ACADEMICALLY UNPROVEN.** This is stated in the README
   and is the central caveat. No part of this audit should be read
   as endorsing the Tc = 300 K candidate.

2. **The repo ships spec + falsifier preregister only.** v1.1.0 is
   book-keeping closure, **not** empirical evidence of RT-SC. The
   §3.1 verdict is **UNCLEAR**, intentionally — not HARD_WALL.

3. **HARD_WALLs (§3.3, §3.8) are procedural / community-norm, not
   physics.** They can be cleared by good experimental design.

4. **48 T at any T is already broken by REBCO at 20 K.** The
   *interesting* claim is "48 T at 300 K with no cryocooler" — that
   is the RT-SC-dependent part. The audit separates these.

5. **No n=6 lattice as a "limit"** per LATTICE_POLICY.md. The
   σ·τ = 48 framing is organising vocabulary; the *real* physics is
   Pauli limit at Tc.

6. **claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) specifically failed §2.8 §3.8** (ferromagnetic impurity
   confound). Future candidates must clear the 4-measurement gate to
   not repeat the failure mode.

---

## §6 References

- `LATTICE_POLICY.md` §1.2 — taxonomy
- `README.md` — RT-SC unproven status, sister substrates (fusion / ufo / cern)
- `rtsc/` — Tc = 300 K candidate spec
- `sc/` — BCS + Abrikosov baseline
- `verify/falsifier_check.hexa` — F-RTSC-{1,2,3} + F-SC-{1,2,3}
- `verify/lint_numerics.hexa` — numerical-claim lint
- `firmware/build/verification_matrix.md` — coil-driver scaffolds
- External: Bardeen-Cooper-Schrieffer (1957), Werthamer-Helfand-Hohenberg
  (Hc2 theory), Lee, Sungyu et al. (2023) *claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) preprint* (and ~12
  failed-replication preprints 2023-Q3/Q4),
  Drozdov et al. (2019) *LaH₁₀ at 250 K under pressure*,
  A-Lab (LBNL, 2023) *Autonomous Inorganic Materials Synthesis*,
  Merchant et al. (2023) *GNoME — Scaling Deep Learning for Materials*.

---

*End of LIMIT_BREAKTHROUGH.md (hexa-rtsc, Wave M).*
