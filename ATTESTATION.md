# hexa-rtsc — DOCS-ONLY ATTESTATION (D116)

> **This sibling repository is docs-only.** All RT-SC verification *substrate*
> (algorithm / implementation code) has migrated to its canonical home in
> **`hexa-lang/stdlib/rtsc/`**. This repo retains design docs, papers,
> empirical-validation fixtures, board artifacts, and governance only.

## Governance basis

- **D116** — sibling repos (`hexa-rtsc/` · `hexa-matter/` · `hexa-bio/` · `hexa-chem/`)
  are docs-only; substrate SSOT lives under `hexa-lang/stdlib/<domain>/`.
- **project.tape `@D d3`** — *implementation code lives in one canonical home*.
  Algorithm / implementation code lives in the canonical stdlib home (per-language
  root); topical sister folders / per-domain repos hold docs · manifests · examples only.

## Code home

| concern | location |
|---|---|
| RT-SC verification substrate (SSOT) | `~/core/hexa-lang/stdlib/rtsc/` |
| design docs · papers · breakthroughs · governance | `~/core/hexa-rtsc/` (this repo) |

## Migration provenance

The substrate migrated via these MERGED hexa-lang PRs:

| PR | scope |
|---|---|
| #281 | `verify/` 4 algorithm files (`calc_bcs` · `calc_hc2_48t` · `calc_mcmillan` · `falsifier_check`) |
| #285 | R2 additional substrate (29 verify files → `verify-additional/`) |
| #286 | `falsifier_dispatch.hexa` (D114 Phase B algorithm · cockpit-born) |
| #293 | consolidate `verify-additional/` → `verify/` (single canonical `verify/` of 33) |
| #298 | 16 stragglers — 9 application verifiers + 6 tests + `install.hexa` + firmware HDL/MCU/EDA |

## What was removed from this repo (68 files · ~14,130 LOC)

Each removed file was verified **byte-identical** (sha-256) against its
`hexa-lang/stdlib/rtsc/` counterpart on `origin/main` before deletion:

- `verify/*.hexa` — 32 (all migrated `verify/` files **except** `falsifier_check.hexa`, see straggler note)
- `firmware/sim/*.hexa` — 4
- `cli/hexa-rtsc.hexa` — 1
- `origins/sc-dse/*.hexa` — 2
- `rtsc/*-verify.hexa` — 10 application verifiers
- `tests/*.hexa` — 6
- `install.hexa` — 1
- `firmware/hdl/{calorimetry_daq.v, quench_detect.v, tb_quench_detect.v, build.tcl, constraints.xdc, Makefile}` — 6
- `firmware/mcu/{calorimetry_drv.rs, chamber_drv.rs, lib.rs, Cargo.toml, memory.x}` — 5
- `firmware/eda/build_kicad.py` — 1

## What stays (genuine docs · D116-compliant)

- `breakthroughs/` · `doc/` · `docs/` · `papers/` · `memory/` · `sc/superconductor.md`
- `verify/fixtures/*.xml` — 6 empirical-validation datasets (test data, NOT code)
- `firmware/eda/*.kicad_*` — board artifacts; `firmware/{Makefile, README, doc/, build/}`;
  `firmware/{hdl,mcu}/.gitignore` (repo-local tooling, not migrated)
- `README*.md` · `CHANGELOG.md` · `CITATION.cff` · `LICENSE` · `LATTICE_POLICY.md`
  · `LIMIT_BREAKTHROUGH.md` · `TAPE-AUDIT.md` · `RELEASE_NOTES_*` · `IMPORTED_FROM_CANON.*`
  · `AGENTS.tape` · `CLAUDE.md` · `hexa.toml` · `.roadmap.hexa_rtsc`

## Straggler — NOT deleted

- **`verify/falsifier_check.hexa`** — NOT byte-identical to the hexa-lang copy.
  The hexa-lang `origin/main` copy still references the pre-scrub `calc_lk99.hexa` /
  `numerics_lk99.hexa` filenames (5 stale `lk99` references), whereas this repo's
  copy is the post-scrub CSH version. Kept here pending a hexa-lang follow-up that
  refreshes `stdlib/rtsc/verify/falsifier_check.hexa` to the scrubbed (CSH) content.
  Once hexa-lang carries the byte-identical scrubbed copy, this file may be removed
  in a follow-up attestation step.

## Pending follow-ups

- **demiurge pointer re-point** (not done in this PR — separate repo, concurrent edits):
  `domains/INDEX.demi:59 substrate_ssot = "~/core/hexa-rtsc/"` and
  `domains/SUBSTRATE_LINKS.demi:48 sibling_path = "~/core/hexa-rtsc/"` should be
  re-pointed / annotated docs-only toward `~/core/hexa-lang/stdlib/rtsc/`.
- **`verify/falsifier_check.hexa`** straggler resolution (see above).
