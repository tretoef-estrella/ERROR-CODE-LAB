# Search Statistics

Comprehensive data from the Error Code Lab campaign, 19–20 February 2026.

## Total Codes Evaluated

| Field | Method | Count | Best d | Target d |
|-------|--------|-------|--------|----------|
| GF(2) | Random QC index 2–5 | ~500K | d = 16 ([43,10]) | 17 |
| GF(2) | BCH subcode search | ~2K | d = 24 ([64,16]) | 25 |
| GF(2) | Kohnert-Zwanzger derivations | ~200 | All match Lb | — |
| GF(3) | Random systematic (3-level pruning) | ~1M | d = 18 ([33,6]) | 19 |
| GF(3) | Genetic algorithm | ~4K (41 gens) | d = 18 | 19 |
| GF(3) | Plateau walk | ~7K steps | d = 18 | 19 |
| GF(3) | Quasi-cyclic (index 3, λ=1) | 222,331 | d = 17 | 19 |
| GF(3) | Quasi-twisted (index 3, λ=2) | 26,939 | d = 18 | 19 |
| GF(3) | Construction XX subcodes | 2,186 (exhaustive) | d = 18 | 19 |
| GF(3) | Column extensions | 5,096 (exhaustive) | d = 18 | 19 |
| GF(4) | Random systematic | ~500 | d = 11 ([22,6]) | 13 |
| GF(4) | QC index 5 + SA | ~3K | d = 19 ([35,7]) | 22 |
| **Total** | | **~2,500,000+** | | |

## Speed Benchmarks

| Engine | Field | k | Speed | Notes |
|--------|-------|---|-------|-------|
| Random + 3-level pruning | GF(3) | 6 | 36,000/s | ChatGPT's design |
| Random + row filter | GF(3) | 6 | 18,000/s | Simpler filter |
| QC index 3 | GF(3) | 6 | 7,939/s | Circulant structure |
| Random systematic | GF(4) | 6 | ~3/s | Pure Python, unoptimized |
| Random systematic | GF(4) | 7 | ~0.3/s | 16K codewords |
| Subcode enumeration | GF(3) | 7→6 | ~340/s | 2186 subcodes in 6.4s |

## ChatGPT's 3-Level Pruning Pipeline

For GF(3), k = 6, n = 33:

| Level | Filter | Rejection Rate | Cost |
|-------|--------|---------------|------|
| 1 | Row weight < d−3 | ~70% | O(k×n) |
| 2 | Pair weight < d | ~90% of survivors | O(k²×n) |
| 3 | Full enumeration (3⁶ = 729 codewords) | Exact | O(3^k × n) |

Only ~3% of random matrices reach Level 3.

## Key Observations

1. **The Lb wall**: Across all fields and targets, random search consistently reaches Lb but never exceeds it. The percentage of random codes achieving d = Lb varies (36% for [33,6]₃) but the percentage achieving d = Lb+1 is always 0%.

2. **Algebraic methods reach Lb deterministically**: Construction XX produces d = 18 exactly as predicted by theory. BCH codes achieve their designed distances. No randomness needed.

3. **The Ub may be illusory**: For [33,6]₃, the Griesmer bound allows d = 19 but our exhaustive analysis of the Construction XX space proves d = 19 is unreachable by this method. The actual optimal distance may be 18.

4. **QT > QC**: Constacyclic (λ=2) codes consistently outperform cyclic (λ=1) codes for the same search effort. For [33,6]₃: QC best = 17, QT best = 18.
