# Verified Generator Matrices

All matrices in this file have been computationally verified by exhaustive codeword enumeration.

## [33, 7, 18] over GF(3) — Construction XX

### Generator Polynomials (BCH ingredients, length 26)

Coefficients in GF(3) = {0, 1, 2}, constant term first.

**C = [26, 7, 14]** BCH(δ=14, b=1):
```
g_C = [2, 0, 1, 0, 1, 0, 1, 1, 2, 1, 1, 2, 0, 0, 1, 2, 0, 1, 2, 1]
```

**C₁ = [26, 4, 17]** BCH(δ=17, b=1):
```
g_C1 = [1, 1, 2, 1, 2, 0, 2, 2, 0, 1, 2, 2, 2, 1, 1, 0, 1, 0, 2, 0, 0, 2, 1]
```

**C₂ = [26, 6, 15]** BCH(δ=15, b=0):
```
g_C2 = [1, 2, 2, 1, 2, 1, 2, 0, 2, 1, 0, 2, 2, 0, 2, 2, 2, 2, 2, 1, 1]
```

### Quotient Polynomials

```
h1 = [2, 2, 0, 1]      (g_C1 = g_C × h1)
h2 = [2, 1]             (g_C2 = g_C × h2)
h_inter = [1, 0, 2, 2, 1]  (h1 × h2)
```

### Coefficient Matrices (subcodes expressed in C's basis)

**M₁** (C₁ as 4-dim subspace of C):
```
[[2, 2, 0, 1, 0, 0, 0],
 [0, 2, 2, 0, 1, 0, 0],
 [0, 0, 2, 2, 0, 1, 0],
 [0, 0, 0, 2, 2, 0, 1]]
```

**M₂** (C₂ as 6-dim subspace of C):
```
[[2, 1, 0, 0, 0, 0, 0],
 [0, 2, 1, 0, 0, 0, 0],
 [0, 0, 2, 1, 0, 0, 0],
 [0, 0, 0, 2, 1, 0, 0],
 [0, 0, 0, 0, 2, 1, 0],
 [0, 0, 0, 0, 0, 2, 1]]
```

**M_inter** (C₁∩C₂ as 3-dim subspace of C):
```
[[1, 0, 2, 2, 1, 0, 0],
 [0, 1, 0, 2, 2, 1, 0],
 [0, 0, 1, 0, 2, 2, 1]]
```

### Weight Distribution of [33, 7, 18]₃

| Weight | Count |
|--------|-------|
| 0 | 1 |
| 18 | 240 |
| 19 | 324 |
| 20 | 162 |
| 21 | 216 |
| 22 | 324 |
| 23 | 162 |
| 24 | 216 |
| 25 | 324 |
| 26 | 162 |
| 27 | 56 |
| **Total** | **2187** |

### GF(27) Arithmetic

Field: GF(3)[x] / (x³ + 2x + 1)

Primitive element: α = (0, 1, 0) with order 26

Element representation: (a₀, a₁, a₂) → a₀ + a₁·α + a₂·α²

## [32, 4, 21] over GF(3) — Belov Code

Constructed from PG(3, 3) by removing two coordinate 2-planes.

Start: Simplex S(4, 3) = [40, 4, 27] (all points of PG(3, 3))
Remove: {(a, b, 0, 0)} ∪ {(0, 0, c, d)} — 8 points total (after excluding origin)
Result: [32, 4, 21]₃

Puncture columns 31–32 to obtain [30, 4, 19]₃.

## [74, 12, 32] over GF(2) — Kohnert-Zwanzger

Generator matrix (systematic form, from codetables.de):

```
Row  0: 1 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 1 0 0 1 1 0 1 1 1 1 0 1 0 1 1 0 1 1 1 1 1 1 0 1 1 1 0 0 0 0 1 1 0 1 0 0 0 0 1 0 0 1 0 1 0 1 1 0 0 0 1 1 0 1 0 1 0
Row  1: 0 1 0 0 0 0 0 0 0 0 0 0 1 1 0 0 0 1 0 1 0 0 1 1 0 1 0 1 1 0 1 0 0 0 1 1 0 0 1 0 0 1 1 1 0 1 1 1 1 1 1 0 0 1 0 0 1 0 0 0 1 1 1 0 1 1 0 0 1 0 0 0 1 0
Row  2: 0 0 1 0 0 0 0 0 0 0 0 0 1 0 1 1 1 0 0 1 1 0 1 0 1 0 0 0 1 0 0 1 0 0 1 0 1 0 1 1 1 0 1 0 0 0 1 1 0 0 1 0 1 0 0 0 1 1 0 0 0 1 1 0 1 0 1 0 1 1 1 1 1 0
Row  3: 0 0 0 1 0 0 0 0 0 0 0 0 0 1 1 1 0 1 1 1 1 0 0 0 0 0 1 1 1 0 0 1 1 1 1 0 0 0 0 0 1 1 0 1 0 1 0 1 0 1 1 1 0 0 1 0 1 0 0 0 0 0 1 1 0 1 0 0 1 1 1 1 1 1
Row  4: 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 1 1 1 1 0 1 0 1 0 1 0 0 0 0 0 0 1 1 1 1 0 1 0 1 0 0 1 1 0 0 1 1 1 0 0 1 1 0 1 0 1 1 0 1 1 0 0 0 0 0 0 1 1 0 1 1 1
Row  5: 0 0 0 0 0 1 0 0 0 0 0 0 1 0 1 1 0 0 1 0 0 1 0 0 1 1 1 0 1 1 0 0 0 1 0 1 0 0 1 0 1 0 1 1 1 1 0 1 0 1 1 0 1 1 1 0 1 1 0 1 0 0 0 1 1 0 0 0 1 0 0 0 1 0
Row  6: 0 0 0 0 0 0 1 0 0 0 0 0 1 0 1 0 1 1 1 1 0 0 0 0 1 1 1 1 0 1 1 1 1 1 0 1 1 0 1 0 1 1 0 0 1 1 1 1 1 1 0 0 0 1 0 1 1 0 0 1 1 0 1 1 0 1 1 1 0 0 0 1 1 1
Row  7: 0 0 0 0 0 0 0 1 0 0 0 0 0 1 1 0 0 1 1 0 1 1 0 1 0 1 0 0 1 0 1 0 0 1 1 1 0 1 0 1 0 0 0 0 1 0 1 1 0 1 1 1 1 1 1 0 0 0 1 1 1 0 0 0 1 1 0 0 0 1 0 1 0 0
Row  8: 0 0 0 0 0 0 0 0 1 0 0 0 1 0 0 1 1 0 0 1 0 0 1 1 1 1 0 0 1 1 0 1 0 1 1 1 0 1 1 1 0 0 0 1 1 1 0 0 1 0 1 0 1 0 0 0 0 1 1 1 1 0 1 0 0 1 0 1 0 0 0 1 1 1
Row  9: 0 0 0 0 0 0 0 0 0 1 0 0 1 0 1 0 0 1 1 1 0 1 0 1 0 0 0 0 0 1 1 1 1 0 0 1 0 0 0 1 0 0 0 0 1 0 0 0 1 0 1 1 0 0 1 1 0 0 1 1 0 1 1 1 0 1 1 1 1 1 1 0 0 1
Row 10: 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 1 1 0 0 1 1 0 0 1 0 0 1 1 0 1 0 1 0 1 0 0 0 1 0 1 1 0 1 1 1 0 0 0 1 1 1 1 1 0 1 1 0 1 0 0 1 1 0 1 0 0 1 0 1 0 1 0 1 0
Row 11: 0 0 0 0 0 0 0 0 0 0 0 1 1 1 0 1 1 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 0 1 1 1 0 0 0 1 0 1 0 0 1 1 0 0 0 1 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 0
```

Derivation chain (all verified):
- [73, 12, 31] ← puncture any single position
- [72, 12, 30] ← puncture any two positions (matches Lb = Ub = 30)
- [73, 11, 32] ← shorten at any single position
- All values match codetables.de exactly
