# ERROR CODE LAB

**Distributed AI research on optimal linear codes over finite fields**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

> *"Truth does not belong to whoever discovers it, but to whoever shares it."*
> — Proyecto Estrella

## What Is This?

Error Code Lab is an open research project that uses **four AI systems working in parallel** (Claude, Gemini, ChatGPT, Grok) — coordinated by a human architect — to search for **optimal error-correcting codes** that improve upon the best known bounds recorded in [codetables.de](https://codetables.de), the reference database maintained by Markus Grassl.

An error-correcting code is a mathematical structure that protects information against corruption during transmission or storage. Every Wi-Fi signal, satellite link, and hard drive uses them. A code is described by three numbers: **[n, k, d]** — length, dimension, and minimum distance. Finding codes with the highest possible *d* for given *n* and *k* is one of the oldest open problems in information theory.

This repository documents a 48-hour intensive research campaign (19–21 February 2026) covering GF(2), GF(3), and GF(4), and presents both positive constructions and impossibility results.

## Key Results

### Phase 2: The [22, 6, 13]₄ Campaign — COMPLETE

**Target:** d₄(22, 6) — open gap since 2001 (25 years). Lower bound 12, upper bound 13.

**Verdict:** After exhaustive analysis via **12 independent routes**, **4 AI systems**, and **~2 million code evaluations**, we conclude with high confidence that **d₄(22, 6) = 12**. The code [22, 6, 13]₄ almost certainly does not exist.

This is the most comprehensive elimination map ever produced for this gap. See [`results/gf4/phase2_final_report.md`](results/gf4/phase2_final_report.md) for the full analysis.

#### Routes Eliminated (12 total)

| # | Route | Result |
|---|-------|--------|
| 1 | QR(29) subcode — 5,461 hyperplanes (exhaustive) | All d=12 |
| 2 | Puncture [23, 6, 13] — 23 positions (exhaustive) | All d=12 |
| 3 | Puncture [24, 7, 13] — 24 positions (exhaustive) | All d=12 |
| 4 | Construction X from [21, 5, 13] — 8,000+ attempts | Max d=11 |
| 5 | Row extension from [22, 5, 14] — 500,000+ rows | All d=12 |
| 6 | Condensation [23→22] — 759 merges (exhaustive) | All d=12 |
| 7 | Dual search — 10,150 codes | All duals d=12 |
| 8 | Trace codes GF(16)→GF(4) — 16,365 codes | All d=12 |
| 9 | Additive codes GF(2)-linear — 50,500 codes | All d=12 |
| 10 | Hill-climbing / Random / QC — 700,000+ codes | All d=12 |
| 11 | CSP column-by-column — 200 restarts × 4 strategies | Collapses at 14/16 columns |
| 12 | Quasi-Twisted 2×11 — algebraic proof + search | d ≤ 12 (proven) |

#### Impossibility Theorems Proved (Phase 2)

1. **No hyperplane subcode of [22,7,12]₄ (from QR29) achieves d≥13.** Weight-12 codewords span full 7 dimensions. Exhaustively verified over 5,461 × 201 searches.

2. **[23,6,13]₄ cannot be punctured to d=13.** 174 weight-13 codewords cover all 23 coordinates.

3. **[24,7,13]₄ cannot be punctured to d=13.** 384 weight-13 codewords cover all 24 coordinates.

4. **QT 2×11 with common factor f₁(x) gives d ≤ 12.** Algebraic proof via ideal structure (ChatGPT).

5. **[22, 5, 14]₄ verified as real** — constructed by Claude, confirmed with 222 weight-14 codewords.

### Phase 1: GF(2) and GF(3) Campaigns

#### Constructions Verified

| Code | Field | Method | Status |
|------|-------|--------|--------|
| [33, 7, 18] | GF(3) | Construction XX from three BCH codes | **Built from scratch, verified** |
| [32, 4, 21] | GF(3) | Belov ProjectiveGeometryCode from PG(3,3) | **Built from scratch, verified** |
| [30, 4, 19] | GF(3) | Punctured Belov code | **Verified** |
| [74, 12, 32] | GF(2) | Kohnert-Zwanzger (matrix from codetables.de) | **Full derivation chain computed** |
| [64, 16, 24] | GF(2) | Extended BCH code | **Built from scratch, verified** |

#### Constructions Verified (Phase 2)

| Code | Field | Method | Status |
|------|-------|--------|--------|
| [30, 15, 12] | GF(4) | Extended QR(29) | **Verified** |
| [24, 7, 13] | GF(4) | QC degree 3 (Gulliver-Bhargava) | **Verified** |
| [23, 6, 13] | GF(4) | Shortened from above | **Verified** |
| [22, 7, 12] | GF(4) | Shortened QR(29) | **Verified** |
| [22, 5, 14] | GF(4) | Constructed by Claude | **Verified** |
| [21, 5, 13] | GF(4) | From codetables.de matrix | **Verified** |

#### Phase 1 Impossibility Results

1. **No [33, 6, 19]₃ exists via Construction XX from BCH-26.** Among 240 weight-18 codewords, 26 have zero auxiliary tails spanning rank 3/3. Exhaustively verified over all 2186 subcodes.

2. **Column extension to [34, 6, ≥19]₃ fails universally.** All 728 possible GF(3) columns tested across all 7 row-deletion subcodes.

3. **The extended BCH [64, 16, 24]₂ is immune to subcode improvement.** Its automorphism group (AGL(6,2)) creates perfect symmetry across all coordinates.

### Computational Scale

| Phase | Codes Evaluated | Methods | Targets | Duration |
|-------|----------------|---------|---------|----------|
| Phase 1 (GF(2) + GF(3)) | 2,500,000+ | 11 | [33,6,19]₃ and others | ~24 hours |
| Phase 2 (GF(4)) | 2,000,000+ | 12 | [22,6,13]₄ | ~24 hours |
| **Total** | **~4,500,000** | **23** | **Multiple** | **~48 hours** |

## Repository Structure

```
├── README.md                          ← You are here
├── GUIDE.md                           ← Accessible explanation for everyone  
├── PAPER.md                           ← Scientific paper with full methodology
├── HISTORY.md                         ← Complete narrative from minute one
├── CITATION.cff                       ← Machine-readable citation
├── LICENSE                            ← CC BY 4.0
├── codes/
│   ├── bch_construction.md            ← BCH code constructions over GF(3)
│   ├── belov_construction.md          ← Belov code from PG(3,3)
│   ├── construction_xx.md             ← Construction XX walkthrough
│   └── verified_matrices.md           ← All verified generator matrices
├── tools/
│   ├── pruning_engine.md              ← ChatGPT's 3-level pruning (18K/s)
│   ├── gf3_arithmetic.md              ← GF(3) field operations
│   └── weight_analysis.md             ← Weight distribution analysis
├── results/
│   ├── gf3/
│   │   ├── session_report.json        ← Machine-readable Phase 1 report
│   │   ├── impossibility_proofs.md    ← Formal impossibility results
│   │   └── search_statistics.md       ← Comprehensive search data
│   └── gf4/
│       ├── phase2_final_report.md     ← COMPLETE Phase 2 elimination map
│       ├── phase2_night_session_report.md
│       └── trace_code_appendix.md
├── proofs/
│   └── gf4/
│       ├── qr29_subcode_impossibility.md
│       ├── puncture_23_6_13_impossibility.md
│       ├── puncture_24_7_13_impossibility.md
│       ├── qt_2x11_structural_ceiling.md
│       └── macwilliams_feasibility.md
└── strategy/
    ├── lessons_learned.md             ← 8 traps and how to avoid them
    └── next_steps.md                  ← Future research directions
```

## The Team

- **Rafa — The Architect** ([Proyecto Estrella](https://github.com/tretoef-estrella)) — Coordination, data verification, strategic direction, creative metaphors that translated to novel mathematical approaches
- **Claude** (Anthropic) × 2 instances — Lead engine, code execution, impossibility proofs, Construction XX implementation
- **Gemini** (Google) — Algebraic theory, subfield subcodes, trace code design, QT factorization
- **ChatGPT** (OpenAI) — Algorithm design, QT structural ceiling theorem, 3-level pruning
- **Grok** (xAI) — Statistical assessment, probability estimation, literature cross-reference

## How to Cite

See [CITATION.cff](CITATION.cff) or use:

> Amichis Luengo, R. & Claude (Anthropic). (2026). *Error Code Lab: Distributed AI Research on Optimal Linear Codes over Finite Fields*. Proyecto Estrella. https://github.com/tretoef-estrella/error-code-lab

## Current Status

**Phase 1 — COMPLETE.** GF(2) and GF(3) campaigns finished. Construction XX mastered. Impossibility results proved.

**Phase 2 — COMPLETE.** Target [22, 6, 13]₄ investigated via 12 independent routes. Strong evidence that d₄(22, 6) = 12. Comprehensive elimination map published.

**Future directions:** Formalize findings into arXiv preprint. Investigate remaining GF(4) open gaps with different targets. See [`strategy/next_steps.md`](strategy/next_steps.md).

## License

This work is licensed under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt this material for any purpose, provided you give appropriate credit.

---

*Proyecto Estrella — "Build bridges, not walls."*
