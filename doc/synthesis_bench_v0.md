# Synthesis Bench v0 — RT-SC Candidate Synthesis Chamber

> Stage-1+ hardware spec, draft. **Out of RSC code-layer scope** per
> `.roadmap.hexa_rtsc §A.6`. This document is the §A.6.1 Stage A
> deliverable: paper-design strengthening, no actual hardware exists.

**Status**: paper design (2026-05-08). No procurement, no fab.
**Owner**: TBD (`.roadmap §A.5` Step-1 collab decision pending —
NIMS / Argonne MSD / 大阪大 / KIAS / SNU CMR cohort).

## §1 WHY

To close `F-RTSC-1` (claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) reproduction failure → next-candidate
substrate spec) at the **strict-T3** tier (recipe §9 empirical), an
in-house synthesis bench is required so the τ(6)=4 reproduction-floor
can be cleared by samples whose provenance + composition + heat-
treatment is fully under our control. Outsourcing synthesis to one of
the §A.6 Step-1 candidate labs is faster but loses the
purity/protocol audit trail that makes failed reproductions
informative.

## §2 ANCHORS (n=6 lattice + .roadmap §A.4 falsifier)

- F-RTSC-1 retract criterion: 0/τ(6)=0/4 confirmed reproductions
  for any candidate (claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim), Cu-Pb-H, hydride family, infinite-layer
  nickelate) within stated synthesis protocol → spec update
- T3 raw-data evidence required: independent labs (≥ τ=4) reproduce
  candidate Tc + Meissner under `.roadmap §A.4 raw_77_rtsc_lk99_repro_v1`
  schema
- σ-φ = 10 false-positive multiplier (numerics_lk99 anchor) — design
  must accommodate ≤ 0.1 confirmation rate without false-positive
  contamination

## §3 BOM (full)

| # | Item | Spec | Vendor (candidate) | Cost (USD) | Note |
|:-:|:-----|:-----|:-------------------|:----------:|:-----|
| 1 | High-pressure cell | 5–20 GPa, ⌀10 mm Belt apparatus | Riken Univ press, Almax | 180k | claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) calls 925°C @ 1 atm; hydride family needs 5–20 GPa |
| 2 | Tube furnace | RT–1500°C, ⌀60 mm bore, 5°C/min ramp | Carbolite STF15/180 | 12k | claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) 925°C heat treatment |
| 3 | Vacuum + Ar atmosphere | 10⁻⁶ mbar base, 5N Ar fill | Pfeiffer HiCube + Praxair Ar | 28k | precursor Pb₃(VO₄)₂ + Cu₃P inert handling |
| 4 | Glovebox | < 0.1 ppm O₂/H₂O, He gas-purifier | MBraun UNILAB Pro | 65k | air-sensitive precursors + post-quench sample storage |
| 5 | Powder XRD | Cu Kα, 2θ 5–120° | Bruker D2 Phaser | 50k | phase confirmation per heat-treatment step |
| 6 | SQUID magnetometer | 1.8–400 K, ± 7 T | Quantum Design MPMS-3 | 600k | Tc + Meissner susceptibility (T3 raw data) |
| 7 | Resistivity rig | 1.5–300 K, 4-probe, 0–9 T | QD PPMS DynaCool | 800k | 4-probe ρ(T) cross-check Tc; F-RTSC-2 McMillan ceiling test |
| 8 | Inert ball mill | tungsten-carbide vials, 1500 rpm | Retsch PM 100 | 18k | precursor mixing (claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) Lanarkite + Cu₃P route) |
| 9 | Optical microscope + Raman | 532 nm, 1 μm spot | Renishaw inVia | 220k | grain-by-grain composition mapping |
|10 | EBSD detector (option) | EDAX TSL OIM 8 | EDAX | 250k | crystallographic orientation per grain (CN=6 vs other) |
|11 | Sample-loading port | UHV-compatible Pb-shielded transfer | custom (in-house) | 8k | radiation-safe Pb-isotope handling |
|12 | DI water + N₂ purge skid | 2 L/min DI, 200 L/min N₂ | Millipore + Praxair | 6k | post-synthesis cleaning |
|13 | Safety: Pb dust extractor | HEPA H14, exhaust to chimney | Camfil Megalam | 14k | Pb apatite synthesis dust hazard |
|14 | Safety: H₂S monitor | 0.1–100 ppm, 4-wire alarm | RKI 03-Series | 3k | Cu₃P + heat may release P₃ vapors |

**Subtotal**: ≈ 2.25 M USD (excluding install + first-year operations).

## §4 Block diagram (ASCII)

```
                    ┌─────────────────────────────────┐
                    │  GLOVEBOX (MBraun UNILAB Pro)  │
                    │  < 0.1 ppm O₂/H₂O, He purifier  │
                    └────────────┬────────────────────┘
                                 │ inert transfer (port #11)
                                 ▼
   ┌────────────┐   ┌────────────────────┐   ┌───────────────────┐
   │ Ball mill  │──▶│  Tube furnace      │──▶│  High-P cell      │
   │ (Retsch    │   │  (Carbolite        │   │  (Belt apparatus, │
   │  PM 100)   │   │   STF15/180)       │   │  5–20 GPa)        │
   └────────────┘   └────┬───────────────┘   └────────┬──────────┘
                         │ 925°C 24 h ramp            │
                         ▼                            ▼
                    ┌─────────────────────────────────────┐
                    │  CHARACTERIZATION SUITE             │
                    │  ┌─────────┐  ┌─────────┐  ┌─────┐ │
                    │  │   XRD   │  │  SQUID  │  │ PPMS│ │
                    │  │ (Bruker)│  │ (MPMS-3)│  │ (QD)│ │
                    │  └─────────┘  └─────────┘  └─────┘ │
                    │  ┌─────────────┐  ┌──────────────┐ │
                    │  │ Raman/Opt   │  │  EBSD (opt)  │ │
                    │  └─────────────┘  └──────────────┘ │
                    └─────────────────────────────────────┘
                                 │
                                 ▼
                       T3 raw-data:
                       Tc(B,T), χ(T), ρ(T), CN per grain
                       → schema raw_77_rtsc_lk99_repro_v1
                       → falsifier_check.hexa F1_T3 closure
```

## §5 Interface table (control + data flow)

| Source | Sink | Protocol | Rate | Note |
|:------|:----|:--------|:----:|:-----|
| Tube furnace temp PT100 | MCU chamber_drv (Stage D) | RS-485 Modbus | 1 Hz | feedback loop for 925°C ± 0.5 K hold |
| High-P cell load cell | MCU chamber_drv | 4-20 mA → 16-bit ADC | 10 Hz | safety-critical (overpressure abort) |
| Glovebox O₂/H₂O sensor | MCU chamber_drv | analog 0-5V | 1 Hz | abort if O₂ > 0.5 ppm during transfer |
| SQUID χ(T) raw | DAQ PC | IEEE-488 GPIB | 100 sps | offline reduction → Tc fit |
| PPMS ρ(T) raw | DAQ PC | TCP/IP (QD bridge) | 1 ksps | F-RTSC-2 McMillan ceiling check |
| XRD diffractogram | DAQ PC | proprietary Bruker | per-scan | XRD pattern matching Pb₁₀Cu(PO₄)₆O |
| Raman spectrum | DAQ PC | USB CDC | per-spot | grain-resolved composition |
| Pb dust extractor flow | facility safety panel | dry contact | continuous | interlock — synthesis aborts if extractor stops |
| H₂S monitor | facility safety panel | 4-wire alarm | continuous | interlock — synthesis aborts at 5 ppm |

## §6 Safety spec

### §6.1 Pb hazard
- Pb apatite (Pb₁₀Cu(PO₄)₆O) generates Pb dust on grinding/quench.
  Class B (radioactive) waste only if Pb-208 isotope source used; for
  natural Pb, ordinary Pb-toxicity protocol applies.
- All grinding/quench in HEPA H14 hood with 0.5 m/s face velocity.
- Operators wear FFP3 respirator + nitrile-over-cotton gloves.

### §6.2 H₂S / P₃ vapor hazard
- Cu₃P heat-treated above 800°C may release P₃ + trace H₂S (with
  moisture). H₂S monitor interlock: synthesis aborts at 5 ppm.

### §6.3 High-pressure cell
- Belt apparatus 5–20 GPa: physical safety enclosure (12 mm steel,
  blast-rated for 50 kJ release). Pressure ramp ≤ 1 GPa/min. Manual
  abort + automatic dump valve at 22 GPa.

### §6.4 Cryogen handling
- SQUID + PPMS: liquid He + N₂. O₂ sensor in cryostat room. Cold-trap
  on dewar exhaust. Operators wear cryogenic gloves + face shield.

### §6.5 Magnetic field hazard
- SQUID 7 T + PPMS 9 T: 5-Gauss line marked. Pacemaker / implant
  exclusion zone painted on floor. No ferromagnetic tools within.

## §7 Verification path (recipe §3 tier ladder)

| Tier | What closes it | Status |
|:-:|:-----------------|:-:|
| T1 algebraic | `verify/calc_lk99.hexa` (n=6 closed-form anchors) | ✓ done |
| T2 numerical | `verify/numerics_lk99{,_parity,_solver}.hexa` (3-stack) | ✓ done |
| T3 archival  | `verify/empirical_lk99_arxiv.hexa` (corpus existence) | ✓ done |
| T3 raw-data  | this bench produces `raw_77_rtsc_lk99_repro_v1` data | **TBD** (needs build) |

The bench above closes **T3 raw-data** for F-RTSC-1 once 4 independent
batches have been synthesized + measured + cross-checked against
candidate Tc claim.

## §8 Build path (Stage-1+ §A.6)

| Step | What | Cost (cum.) | Time |
|:-:|:-----|:-----------:|:----:|
| 0 | This document (Stage A) | $0 | 1 d ✓ |
| 1 | Detailed engineering drawings + vendor quotes | $20k | 2 mo |
| 2 | Procurement (BOM #1–14) | $2.25M | 6 mo |
| 3 | Install + commissioning | $300k | 3 mo |
| 4 | First synthesis (claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) baseline batch ×4) | $50k/yr ops | 1 mo |
| 5 | Independent-lab cross-verify (NIMS / Argonne / 大阪大) | TBD | 12 mo |

Total to **F-RTSC-1 strict-T3 closure**: ≈ $2.6M + 22 months from
funding-release date.

## §9 Open questions (→ §A.5 pending decisions)

- Lanarkite vs Misenite vs Pyromorphite as Pb-source precursor
  (synthesis route SLA, `.roadmap §A.5 negative-result granularity`).
- Cu₃P stoichiometry: x=0.9 vs x=1.1 in Pb₁₀₋ₓCuₓ(PO₄)₆O — affects
  Cu site occupancy.
- 925°C vs 950°C heat-treatment — original claim-only RT-SC (anonymized 2026-05-22 from a specific historical claim) group claimed 925°C
  exact, reproductions tested 900–960°C.
- Quench rate: water-quench vs furnace-cool — affects oxygen
  stoichiometry.

## §10 Cross-references

- `.roadmap.hexa_rtsc §A.4` falsifier preregister (F-RTSC-1)
- `.roadmap.hexa_rtsc §A.6.1 Stage A` (this doc is the Stage A deliverable)
- `verify/numerics_lk99_solver.hexa` (T2 ×3 closed-form solver)
- `verify/empirical_lk99_arxiv.hexa` (T3 archival anchor)
- Sister: `~/core/hexa-cern doc/benchtop_v0_design.md` (analogous spec)

---

**Authority**: §A.6.1 Stage A paper-design strengthening per
recipe §9 honest framing. This document is the spec from which BOM #1–14
will be procured at §A.6 Step 2 (funding round) → Step 4 (Stage-2/3 build).
