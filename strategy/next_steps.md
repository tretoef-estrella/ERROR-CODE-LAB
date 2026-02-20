# Next Steps: The Hunt for [22, 6, 13] over GF(4)

## Target

| Parameter | Value |
|-----------|-------|
| Field | GF(4) = {0, 1, ω, ω²} |
| Length | n = 22 |
| Dimension | k = 6 |
| Current Lb | 12 |
| Upper bound | 13 (Griesmer) |
| Gap | 1 |
| Goal | Find d ≥ 13 |

## Attack Strategy

### Primary Vector: Subcode Search from [22, 7, 12]

The [22, 7, 12] over GF(4) is **closed** (Lb = Ub = 12). Its generator matrix exists as a well-defined mathematical object.

If ANY dimension-6 subcode of this code has minimum distance ≥ 13, we obtain a [22, 6, 13] and close the gap.

**Construction path** (identified by Grok):

1. Start with the **quadratic residue (QR) code** of length 29 over GF(4)
   - Cyclic code with length 29 (prime)
   - Order of 4 mod 29 is 14
   - QR set: {1, 4, 5, 6, 7, 9, 10, 11, 13, 16, 17, 19, 20, 22, 24, 25, 28}
2. **Extend** to [30, 15, 12] by adding a parity check position
3. **Shorten** at 8 positions (23–30) to obtain [22, 7, 12]

### Search Space

- A dimension-6 subcode is defined by ker(v) for v ∈ GF(4)⁷ \ {0}
- Total hyperplanes: (4⁷ − 1) / (4 − 1) = 5461 (projective count)
- Or directly: 4⁷ − 1 = 16383 vectors, each defining a dim-6 subcode
- Each subcode has 4⁶ = 4096 codewords
- Total verification time: ~16K × 4K × (fast bitwise ops) = feasible in minutes

### Speed Requirements

**Gemini's bit-packing design** (critical for speed):
- Each GF(4) symbol = 2 bits
- A codeword of length 22 = 44 bits, fits in one `uint64`
- Multiplication by ω: bit-swap + XOR
- Hamming weight: `(C | (C >> 1)) & 0x555...` then popcount
- Gray code enumeration: one XOR per codeword

Target: 10,000+ subcodes verified per second.

### Fallback Vectors

If no subcode of [22, 7, 12] has d ≥ 13:

1. **Different [22, 7, 12] codes**: The QR construction gives one specific code. Other [22, 7, 12] codes may exist (via different shortening positions or non-equivalent constructions)
2. **Direct algebraic construction**: Trace codes from GF(64) restricted to GF(4), as outlined by Gemini
3. **Quasi-cyclic search**: 22 = 2 × 11, so QC index 2 with 11×11 circulant blocks over GF(4)
4. **Different targets**: [23, 7, 13], [30, 6, 19], [26, 7, 15] — all have gap = 1 over GF(4)

## All GF(4) Open Gaps (Verified February 20, 2026)

### Fast targets (k ≤ 7)

| [n, k] | Lb | Ub | Need d ≥ |
|--------|----|----|----------|
| **[22, 6]** | **12** | **13** | **13** ← PRIMARY |
| [30, 6] | 18 | 19 | 19 |
| [23, 7] | 12 | 13 | 13 |
| [26, 7] | 14 | 15 | 15 |
| [27, 7] | 15 | 16 | 16 |
| [29, 7] | 16 | 17 | 17 |
| [30, 7] | 17 | 18 | 18 |

### Slow targets (k = 8)

| [n, k] | Lb | Ub | Need d ≥ |
|--------|----|----|----------|
| [19, 8] | 8 | 9 | 9 |
| [24, 8] | 12 | 13 | 13 |
| [25, 8] | 12 | 13 | 13 |
| [26, 8] | 13 | 14 | 14 |
| [27, 8] | 14 | 15 | 15 |
| [28, 8] | 15 | 16 | 16 |
| [30, 8] | 16 | 17 | 17 |

## What We Bring from the GF(3) Campaign

Every lesson transfers:
1. **No random search** — algebraic seeds only
2. **Weight analysis first** — count weight-d codewords before searching subcodes
3. **Single coordinate system** — no RREF mixing
4. **Sprints with checkpoints** — 30s max, save state
5. **Exhaustive subcode enumeration** — the space is small enough (5461 hyperplanes)
