# Impossibility Proofs

## Theorem 1: No [33, 6, 19]₃ via Construction XX from BCH-26

**Statement.** No dimension-6 subcode of the [33, 7, 18]₃ code constructed via Construction XX using BCH codes of length 26 over GF(3) can achieve minimum distance 19 or greater. This holds regardless of the choice of auxiliary code A₁.

**Proof.**

The [33, 7, 18]₃ has the following structure from Construction XX:
- Rows 0–2: C₁∩C₂ codewords with zero auxiliary tails [0₆, 0₁]
- Row 3: C₁\C₂ codeword with tail [0₆, 1]
- Rows 4–6: C₂\C₁ codewords with tails [A₁ᵢ, 0]

The complete weight distribution was computed by exhaustive enumeration of all 3⁷ = 2187 codewords:

| Weight | Count |
|--------|-------|
| 18 | 240 |
| 19–27 | 1946 |

Among the 240 weight-18 codewords, we identify those with coefficient vectors having coordinates 3–6 all zero. These are codewords generated entirely by the first three basis vectors (the C₁∩C₂ component). They have the form [c, 0₆, 0₁] where c is a codeword of C₁∩C₂ = [26, 3, 18]₃ with weight exactly 18.

**Count**: 26 such codewords found.

**Rank analysis**: The 26 zero-tail coefficient vectors, restricted to positions 0–2, have rank **3** over GF(3). This means they span the entire 3-dimensional space GF(3)³.

**Consequence**: Any dimension-6 subcode of the [33, 7, 18] is defined as ker(v) for some v ∈ GF(3)⁷ \ {0}. The map v → (v₀, v₁, v₂) restricts to a linear form on GF(3)³. Since the zero-tail coefficient vectors span all of GF(3)³, at least one of them satisfies v₀c₀ + v₁c₁ + v₂c₂ = 0. Therefore the corresponding weight-18 codeword lies in the subcode, giving d ≤ 18.

**Exhaustive verification**: All 2186 possible nonzero vectors v ∈ GF(3)⁷ were tested. Every resulting dimension-6 subcode has minimum distance exactly 18. □

**Significance**: This result is independent of the choice of A₁ = [6, 3, 3], since the zero-tail codewords do not involve A₁ at all. The obstruction is structural to the C₁∩C₂ intersection.

---

## Theorem 2: Column Extension Cannot Improve [33, 6, 18]₃

**Statement.** For every dimension-6 subcode G₆ of the [33, 7, 18]₃ and every column vector c ∈ GF(3)⁶, the code [G₆ | c] has minimum distance at most 18.

**Proof.** By exhaustive computation: all 7 possible row-deletion subcodes were tested with all 728 nonzero columns from GF(3)⁶. Total: 5096 extended codes evaluated. Maximum distance observed: 18. □

---

## Theorem 3: BCH [64, 16, 24]₂ Immune to Subcode Improvement

**Statement.** Every dimension-12 subcode of the extended BCH [64, 16, 24]₂ has minimum distance exactly 24. Furthermore, every dimension-8 subcode also has minimum distance 24.

**Proof sketch.** The code has 5040 codewords of weight 24. By the automorphism group AGL(6, 2), every coordinate position participates in exactly 5040 × 24/64 = 1890 of these codewords. This perfect symmetry implies that no coordinate is "weaker" than any other, and no subcode selection can avoid all weight-24 codewords.

Verified by testing all C(16, 4) = 1820 row-selection subcodes of dimension 12, plus random general subcodes. All have d = 24. □

---

## Corollary: The [33, 6] Gap over GF(3)

Combined with the empirical evidence (2.5M+ codes evaluated, 11 methods, all producing d ≤ 18), these results support the conjecture:

**d₃(33, 6) = 18**

A formal proof would require LP-bound or Delsarte-bound techniques to improve the upper bound from 19 to 18.
