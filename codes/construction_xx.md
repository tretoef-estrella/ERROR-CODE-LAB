# Construction XX Walkthrough: Building [33, 7, 18]₃ from Scratch

This document walks through the complete construction, from GF(27) arithmetic to the final verified code.

## Step 1: GF(27) Field Arithmetic

GF(27) = GF(3)[x] / (x³ + 2x + 1)

Elements are triples (a₀, a₁, a₂) ∈ GF(3)³, representing a₀ + a₁α + a₂α².

Primitive element: α = (0, 1, 0), order 26.

Multiplication: polynomial multiplication modulo x³ + 2x + 1, with coefficient reduction modulo 3.

## Step 2: BCH Generator Polynomials

For each BCH code, we compute the generator polynomial g(x) as the product of minimal polynomials of consecutive powers of α.

### Cyclotomic cosets modulo 26 over GF(3):
- Powers of 3 modulo 26 cycle as: i → 3i mod 26
- Example: coset of 1 = {1, 3, 9} (since 3³ = 27 ≡ 1 mod 26)

### Minimal polynomials:
Each cyclotomic coset of size s contributes a degree-s irreducible factor of x²⁶ − 1 over GF(3).

### Generator polynomial construction:
- g_C: product of minimal polynomials of α¹ through α¹³ → degree 19, giving k = 26 − 19 = 7
- g_C₁: product of minimal polynomials of α¹ through α¹⁶ → degree 22, giving k = 4
- g_C₂: product of minimal polynomials of α⁰ through α¹⁴ → degree 20, giving k = 6

## Step 3: Verify Containment

The key divisibility relations:
```
g_C₁ = g_C × [2, 2, 0, 1]     (h₁, degree 3)
g_C₂ = g_C × [2, 1]            (h₂, degree 1)
```

Verification: polynomial multiplication over GF(3) confirms exact match.

Root analysis:
```
C  roots: {1,2,3,4,5,6,7,8,9,10,11,12,13,15,18,19,20,21,24}
C₁ roots: C ∪ {14, 16, 22}
C₂ roots: C ∪ {0}
```

Since C₁ and C₂ have strictly more roots than C, their generator polynomials are multiples of g_C, confirming C ⊃ C₁ and C ⊃ C₂.

## Step 4: The Soldadura (Basis Alignment)

### The Problem
Generator matrices built from polynomial shifts:
```
G_C:  row i = x^i · g_C(x)     for i = 0,...,6
G_C₁: row i = x^i · g_C₁(x)   for i = 0,...,3
G_C₂: row i = x^i · g_C₂(x)   for i = 0,...,5
```

Each row of G_C₁ is a linear combination of rows of G_C (since C₁ ⊂ C). The coefficients come directly from h₁:

```
G_C₁[i] = h₁[0]·G_C[i] + h₁[1]·G_C[i+1] + h₁[2]·G_C[i+2] + h₁[3]·G_C[i+3]
         = 2·G_C[i] + 2·G_C[i+1] + 0·G_C[i+2] + 1·G_C[i+3]
```

This gives the coefficient matrix M₁ (4×7 over GF(3)) without any RREF computation.

### The Solution
Build an ordered basis in coefficient space GF(3)⁷:

1. **First 3 vectors**: M_inter rows (spanning C₁∩C₂ in coefficient space)
2. **Vector 4**: From M₁, linearly independent of the first 3
3. **Vectors 5–7**: From M₂, extending to full rank 7

Transform to codewords: `G_ordered = T × G_C` where T is the 7×7 change-of-basis matrix.

## Step 5: Subcode Verification

```
C₁∩C₂ (rows 0–2):     d = 18  ✓  (need ≥ d_C + δ_A₁ + δ_A₂ = 14+3+1 = 18)
C₁ (rows 0–3):         d = 17  ✓  (need ≥ d_C₁ + δ_A₂ = 17+1 = 18? Actually need 17)
C₂ (rows 0–2, 4–6):    d = 15  ✓  (need ≥ d_C₂ + δ_A₁ = 15+3 = 18? Actually need 15)
C (all 7):              d = 14  ✓  (need ≥ d_C = 14)
```

## Step 6: Assembly

| Rows | Group | Main (26 cols) | A₁ (6 cols) | A₂ (1 col) |
|------|-------|----------------|-------------|-------------|
| 0–2 | C₁∩C₂ | G_ord[0:3] | **0** | **0** |
| 3 | C₁\C₂ | G_ord[3] | **0** | **1** |
| 4–6 | C₂\C₁ | G_ord[4:7] | **G_A₁** | **0** |

## Step 7: Distance Bound

```
d ≥ min(d_C + δ_A₁ + δ_A₂, d_C₁ + δ_A₂, d_C₂ + δ_A₁)
  = min(14 + 3 + 1, 17 + 1, 15 + 3)
  = min(18, 18, 18)
  = 18
```

All three terms equal 18 — a perfectly balanced construction.

## Step 8: Verification

Exhaustive enumeration of all 3⁷ = 2187 codewords confirms d = 18 exactly.
