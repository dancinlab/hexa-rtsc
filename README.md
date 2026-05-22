<p align="center">
  <img src="docs/logo.svg" width="140" alt="hexa-rtsc">
</p>

<h1 align="center">🧊 hexa-rtsc</h1>

<p align="center"><strong>HEXA-RT-SC Family</strong> — room-temperature superconductor · 48T SC coil · substrate-of-substrates · n=6 closed form</p>

<p align="center">
  <a href="LICENSE"><img alt="License" src="https://img.shields.io/badge/license-MIT-blue"></a>
  <a href=".github/workflows/lint.yml"><img alt="CI" src="https://github.com/dancinlab/hexa-rtsc/actions/workflows/lint.yml/badge.svg"></a>
  <img alt="Version" src="https://img.shields.io/badge/version-1.1.0-success">
  <img alt="Closure" src="https://img.shields.io/badge/closure-100%25-informational">
  <img alt="Lint" src="https://img.shields.io/badge/lint-113%2F113-informational">
  <img alt="Falsifier" src="https://img.shields.io/badge/falsifier-43%2F43-informational">
  <img alt="Firmware" src="https://img.shields.io/badge/firmware-70%2F70-informational">
  <a href="https://doi.org/10.5281/zenodo.20102616"><img alt="DOI" src="https://zenodo.org/badge/DOI/10.5281/zenodo.20102616.svg"></a>
  <img alt="Downstream" src="https://img.shields.io/badge/downstream-hexa--fusion%20·%20hexa--ufo%20·%20hexa--cern-blueviolet">
</p>

<p align="center">Room-temperature superconductor · Meissner · 48T coil · BCS · Abrikosov · CSH-retracted negative anchor · n=6 lattice · falsifier-preregister</p>

---

> **Room-Temp Superconductor — Meissner + 48T SC coil. Substrate-of-substrates for fusion · UFO · accelerator.**
>
> 2-verb energy substrate organized around the **n=6 invariant lattice**:
> RTSC (Tc=300K, Hc2=σ·τ=48T, Cooper φ=2) / SC (BCS, Abrikosov CN=6).
> v1.0.0 ships **spec + falsifier preregister** only — no working empirical
> sandbox. RT-SC is **academically unproven** (canonical retracted claim:
> CSH, Snider et al. Nature 586:373, retracted Nature 610:804 (2022)).

---

## Why

`hexa-rtsc` is the **substrate-of-substrates**: the n=6 base substrate that
three sister substrates depend on:

- **dancinlab/hexa-fusion** — needs **48T SC coil** (σ·τ=48 satisfies confinement gate)
- **dancinlab/hexa-ufo** — needs **Stage-1 Meissner levitation** (B-field expulsion)
- **dancinlab/hexa-cern** — needs **SC magnet** (accelerator beamline bending)

If RT-SC is empirically realised, all three downstream substrates unlock at
once: tabletop fusion, room-temp magnetic levitation, and benchtop accelerator
beamlines. If it is not, all three remain upper-bounded by current
liquid-helium-cooled cuprate / Nb-Ti / Nb₃Sn limits.

This repo extracts the n=6 closed-form candidate spec + falsifier preregister
from `canon/domains/energy/{room-temp-sc,superconductor}/` (SHA
`c0f1f570`, 2026-05-06).

---

## Status

> **RT-SC is academically UNPROVEN.** The canonical negative anchor in this
> repo is **CSH** (carbonaceous sulfur hydride, Snider et al. Nature 586:373
> (2020), retracted Nature 610:804 (2022); susceptibility analysis Hirsch
> Physica C 601:1354118 (2022)). Subsequent room-temp candidates have
> **not been independently replicated**. v1.1.0 ships
> RSC code-layer FINAL (book-keeping closure) per `.roadmap §A.6`:
>
> - n=6 **closed-form candidate** spec (Tc=300K, Hc2=σ·τ=48T, Cooper φ=2 boson, Abrikosov CN=6)
> - **falsifier preregister** tables (F-RTSC-{1,2,3} + F-SC-{1,2,3})
> - **35 verify scripts** (T1 ×6 + T2 ×17 + T3 ×6 + meta ×3 + run_all + cross-cutters; meta = falsifier_check + lint_numerics + saturation_check; T2 includes numerics_cross_pillar 4-pillar consistency)
> - **100% bookkeeping closure** for all 6 falsifiers (T1 + T2 ×3 + T3-archival ×1)
> - **§A.6.1 Phase A → D+ COMPLETE** — 3 hardware design docs, 3 sim-parity
>   scripts, 4 sim-firmware, HDL+MCU verified-build (70/70 PASS)
> - **CHIP DESIGN + SCHEMATICS + PINOUT** — `firmware/doc/` documents
>   STM32F407VGT6 + Artix-7 XC7A35T pin assignments, 11-IC silicon BOM,
>   ASCII signal-path schematics, 7.6 W power budget, 4-layer FR-4 PCB
>
> 🎯 100% closure ≠ RT-SC physics settled. Strict raw-data T3 (Stage-1+
> hardware: synthesis bench + 48 T coil + calorimetry rig) → §A.6 Step 4
> (~$225k + 14-20 mo from funding release).
>
> No empirical claim of working RT-SC is made or implied. Synthesis-side
> validation is out-of-repo (would require a materials lab).

Verdict: **bookkeeping closure 100 %**, empirical claim **NOT verified**.
The lattice machinery + sim parity + sim-firmware + HDL/MCU build are
fully wired: 35 verify/*.hexa scripts + 4 sim-firmware + 12/12 iverilog
testbench + 15/15 cargo unit tests pass end-to-end. Per `.own` own 2:
a `__HEXA_RTSC_*__ PASS` sentinel **never** validates the empirical
RT-SC claim — only that the closed form is regression-locked at the
code-layer for future bench comparison.

```
verify/    35 scripts  (T1×6 + T2×17 + T3-archival×6 + meta×3 + run_all)
           ├─ T2 ×17: 4 closed-form + 4 parity + 4 solver + claim_class_dft + tdgl + whh
           │          + lattice_arithmetic + cross_pillar  (recipe §1 #7+#13)
           └─ meta×3: falsifier_check + lint_numerics + saturation_check (recipe §7.3)
build/     pandoc + xelatex PDF rebuild (Makefile + header.tex; recipe §1 #12)
docs/      numerics_methodology.md — T1/T2/T3/T4 ladder narrative (recipe §1 #13)
firmware/  10 sources  (4 sim + 2 HDL + tb + 3 MCU + lib)
doc/       3 specs     (synthesis_bench / 48t_rebco_coil / calorimetry_rig)
.roadmap   §A.6 + §A.6.1 Stage-1+ hardware path tracked
─────────────────────────────────────────────────────────────────
70/70 firmware tests  +  113/113 lint  +  43/43 falsifier  =  226/226 PASS
```

---

## Install

```bash
# 1. Install hexa-lang (gives you `hexa` + `hx` package manager)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/dancinlab/hexa-lang/main/install.sh)"

# 2. Install hexa-rtsc
hx install hexa-rtsc
```

## Run

```bash
hexa-rtsc rtsc       # room-temp superconductor (Tc=300K, 48T)    [SPEC]
hexa-rtsc sc         # superconductor (BCS / Abrikosov)            [SPEC]
hexa-rtsc status     # 0/2-wired verb table + verdict + caveats
hexa-rtsc lattice    # live-compute n=6 closed-form (σ τ φ Hc2 master)
hexa-rtsc verify     # run all verify/*.hexa invariant audits
hexa-rtsc selftest   # sentinel sweep (specs + own_v1 + verify/ landing)
```

---

## Repo layout

```
hexa-rtsc/
├── README.md                     ← this file (public landing)
├── README.ai.md                  ← AI-native handoff (raw 271)
├── LICENSE                       ← MIT
├── CHANGELOG.md
├── RELEASE_NOTES_v1.0.0.md
├── .own                          ← project-local SSOT (mk2 own_v1) — n=6 lattice + falsifier + code-scope
├── .roadmap.hexa_rtsc            ← cross-cutting tracker — release cadence + falsifier preregister
├── hexa.toml                     ← package manifest (entry/[[bin]] auto-detected by hx)
├── install.hexa                  ← hx pre/post hook
├── cli/
│   └── hexa-rtsc.hexa            ← single-entry router (status / lattice / verify / selftest / rtsc / sc)
├── rtsc/                         ← T1 SPEC — extracted from n6-arch domains/energy/room-temp-sc/
│   ├── room-temp-sc.md
│   ├── *-verify.hexa             ← 10 application shells (move to module/applications/ in v1.1.0)
│   ├── arxiv-metadata.json
│   └── osf-metadata.json
├── sc/                           ← T1 SPEC — extracted from n6-arch domains/energy/superconductor/
│   └── superconductor.md
├── verify/                       ← runnable invariant audit (.hexa, hexa stdlib only)
│   ├── lattice_check.hexa        ← n=6 master identity (10/10 PASS expected)
│   ├── cross_doc_audit.hexa      ← cross-document lattice + falsifier presence (8/8)
│   ├── falsifier_check.hexa      ← F-RTSC/F-SC monotonicity (19/19)
│   └── run_all.hexa              ← orchestrator
├── tests/                        ← hexa native test runner
│   ├── test_selftest.hexa        ← sentinel sweep
│   ├── test_lattice.hexa         ← exercises verify/lattice_check
│   ├── test_verify.hexa          ← exercises verify/run_all
│   └── test_falsifier.hexa       ← exercises verify/falsifier_check
└── doc/
    └── lineage/
        └── origin.md             ← provenance manifest (n6-arch SHA, file-by-file)
```

The `core/<feature>/` + `module/<feature>/` + `README.ai.md` triplet
follows **hive raw.mk2 arch.001** — the canonical core-hierarchy pattern
shared with sister substrates `hexa-sscb` (compute axis, doc-first) and
`hexa-bio` (molecular toolkit). v1.0.0 keeps `rtsc/` + `sc/` flat; v1.1.0
will split them into `core/rtsc/` + `core/sc/` + `module/applications/`
per `.own` own 3 + `doc/lineage/origin.md` migration plan.

---

## Provenance

- RTSC spec **imported** from `canon/domains/energy/room-temp-sc/`
  (SHA `c0f1f570`, 2026-05-06).
- SC spec **imported** from `canon/domains/energy/superconductor/`
  (SHA `c0f1f570`, 2026-05-06).
- CLI dispatcher created **fresh** at extraction; `lattice` + `verify`
  subcommands wired 2026-05-07.
- Structural pattern (.own + README.ai.md + verify/ + doc/lineage/)
  aligned to `hexa-sscb` mk2 own_v1 on 2026-05-07.
- Sister-of-substrates extraction template: `hexa-bio` v1.0.0
  (dancinlab/hexa-bio, 2026-05-04).
- Full file-by-file provenance: [`doc/lineage/origin.md`](doc/lineage/origin.md).

---

## License

MIT. See [LICENSE](LICENSE).

---

## Cross-links

- Sister standalone: [`hexa-bio v1.0.0`](https://github.com/dancinlab/hexa-bio) (Molecular Toolkit substrate)
- Downstream consumer: [`hexa-fusion`](https://github.com/dancinlab/hexa-fusion) (48T SC coil dep)
- Downstream consumer: [`hexa-ufo`](https://github.com/dancinlab/hexa-ufo) (Meissner levitation dep)
- Downstream consumer: [`hexa-cern`](https://github.com/dancinlab/hexa-cern) (SC magnet dep)
- Upstream concept SSOT: `canon/domains/energy/room-temp-sc/room-temp-sc.md`
- Upstream concept SSOT: `canon/domains/energy/superconductor/superconductor.md`
