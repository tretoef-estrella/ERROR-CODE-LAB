# ERROR CODE LAB

**Distributed AI research on optimal linear codes over finite fields**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

> *"Truth does not belong to whoever discovers it, but to whoever shares it."*
> — Proyecto Estrella

## What Is This?

Error Code Lab is an open research project that uses **four AI systems working in parallel** (Claude, Gemini, ChatGPT, Grok) — coordinated by a human architect — to search for **optimal error-correcting codes** that improve upon the best known bounds recorded in [codetables.de](https://codetables.de), the reference database maintained by Markus Grassl.

An error-correcting code is a mathematical structure that protects information against corruption during transmission or storage. Every Wi-Fi signal, satellite link, and hard drive uses them. A code is described by three numbers: **[n, k, d]** — length, dimension, and minimum distance. Finding codes with the highest possible *d* for given *n* and *k* is one of the oldest open problems in information theory.

This repository documents a 48-hour intensive research campaign (19–20 February 2026) covering GF(2), GF(3), and GF(4), and presents both positive constructions and impossibility results.

## Key Results

### Constructions Verified

| Code | Field | Method | Status |
|------|-------|--------|--------|
| [33, 7, 18] | GF(3) | Construction XX from three BCH codes | **Built from scratch, verified** |
| [32, 4, 21] | GF(3) | Belov ProjectiveGeometryCode from PG(3,3) | **Built from scratch, verified** |
| [30, 4, 19] | GF(3) | Punctured Belov code | **Verified** |
| [74, 12, 32] | GF(2) | Kohnert-Zwanzger (matrix from codetables.de) | **Full derivation chain computed** |
| [64, 16, 24] | GF(2) | Extended BCH code | **Built from scratch, verified** |

### Impossibility Theorems Proved

1. **No [33, 6, 19]₃ exists via Construction XX from BCH-26.** Among 240 weight-18 codewords in the [33,7,18], 26 have zero auxiliary tails and span all 3 dimensions of the intersection subspace. Every dimension-6 hyperplane contains at least one. Exhaustively verified over all 2186 possible subcodes.

2. **Column extension to [34, 6, ≥19]₃ fails universally.** All 728 possible GF(3) columns tested across all 7 row-deletion subcodes. Maximum distance remains 18.

3. **The extended BCH [64, 16, 24]₂ is immune to subcode improvement.** Its automorphism group (AGL(6,2)) makes every coordinate equivalent. All 5040 weight-24 codewords distribute with perfect symmetry (1890 per coordinate). No dimension-12 subcode avoids them.

### Empirical Findings

- Over **2.5 million codes evaluated** across GF(2), GF(3), and GF(4)
- **11 distinct search methods** tested (random, genetic, plateau walk, QC, QT, Construction X, Construction XX, column extension, puncturing, shortening, subcode enumeration)
- Random search consistently reaches the known lower bound (Lb) but **never exceeds it** — the Lb→Ub gap requires algebraic structure
- For [33, 6]₃: 36% of random codes achieve d=18 (the Lb), but 0% reach d=19

## Repository Structure

```
├── README.md                  ← You are here
├── GUIDE.md                   ← Accessible explanation for everyone
├── PAPER.md                   ← Scientific paper with full methodology
├── HISTORY.md                 ← Complete narrative from minute one
├── EXECUTIVE_SUMMARY.md       ← Summary for the AI team (Gemini, ChatGPT, Grok)
├── CITATION.cff               ← Machine-readable citation
├── LICENSE                    ← CC BY 4.0
├── codes/
│   ├── bch_construction.md    ← BCH code constructions over GF(3)
│   ├── belov_construction.md  ← Belov code from PG(3,3)
│   ├── construction_xx.md     ← Construction XX walkthrough
│   └── verified_matrices.md   ← All verified generator matrices
├── tools/
│   ├── pruning_engine.md      ← ChatGPT's 3-level pruning (18K/s)
│   ├── gf3_arithmetic.md      ← GF(3) field operations
│   └── weight_analysis.md     ← Weight-18 avoidance analysis
├── results/
│   ├── session_report.json    ← Machine-readable final report
│   ├── impossibility_proofs.md← Formal impossibility results
│   └── search_statistics.md   ← Comprehensive search data
└── strategy/
    ├── lessons_learned.md     ← 8 traps and how to avoid them
    └── next_steps.md          ← Roadmap for [22,6,13] over GF(4)
```

## The Team

- **Rafa — The Architect** ([Proyecto Estrella](https://github.com/tretoef-estrella)) — Coordination, data verification, strategic direction. Psychology graduate from Universidad Complutense de Madrid, currently training for a truck driving license (C category + ADR). Not an expert in anything, but knows a little about everything. Based in Madrid, Spain.
- **Claude** (Anthropic) — Lead engine, code execution, Construction XX implementation
- **Gemini** (Google) — Algebraic theory, subfield subcodes, trace code design, diagnosed the critical "soldadura" (basis alignment) bug
- **ChatGPT** (OpenAI) — Algorithm design, 3-level pruning pipeline, mutation operators, proposed Vector D (subcode enumeration)
- **Grok** (xAI) — Code execution, QR code construction path for GF(4), codetables.de verification

## How to Cite

See [CITATION.cff](CITATION.cff) or use:

> Amichis Luengo, R. & Claude (Anthropic). (2026). *Error Code Lab: Distributed AI Research on Optimal Linear Codes over Finite Fields*. Proyecto Estrella. https://github.com/tretoef-estrella/error-code-lab

## Current Status

**Phase 1 complete** — GF(2) and GF(3) campaigns finished. Construction XX mastered. Impossibility results proved.

**Phase 2 starting** — Target: **[22, 6, 13] over GF(4)**. Attack vector: subcode search within the closed [22, 7, 12] code (extended QR code of length 29). See [next_steps.md](strategy/next_steps.md).

## License

This work is licensed under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt this material for any purpose, provided you give appropriate credit.

---

*Proyecto Estrella — "Build bridges, not walls."*
