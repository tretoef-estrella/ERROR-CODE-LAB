# BCH Code Construction over GF(3)

## Overview

BCH (Bose-Chaudhuri-Hocquenghem) codes of length n = 26 = 3³ − 1 over GF(3) use roots in the extension field GF(27) = GF(3³).

## GF(27) Setup

**Primitive polynomial**: x³ + 2x + 1 over GF(3)

**Element representation**: Each element of GF(27) is a triple (a₀, a₁, a₂) ∈ GF(3)³, representing a₀ + a₁α + a₂α².

**Primitive element**: α = (0, 1, 0), satisfying α³ = α + 1 (equivalently α³ + 2α + 1 = 0 in GF(3)).

**Powers of α**: α has order 26 in GF(27)*. The 26 nonzero elements are α⁰, α¹, ..., α²⁵.

## Cyclotomic Cosets

For GF(3) codes of length 26, the cyclotomic coset of i is {i, 3i mod 26, 9i mod 26} (since 3³ = 27 ≡ 1 mod 26, cosets have size dividing 3).

Each coset corresponds to a minimal polynomial of degree equal to the coset size.

## Codes Used in Construction XX

| Code | Designed distance δ | Starting root b | Generator degree | Dimension k | Actual d |
|------|-------------------|-----------------|-----------------|-------------|----------|
| C | 14 | 1 | 19 | 7 | 14 |
| C₁ | 17 | 1 | 22 | 4 | 17 |
| C₂ | 15 | 0 (= 26) | 20 | 6 | 15 |

Note: C₂ uses starting root b = 0 (i.e., α⁰ = 1), not b = 1. This means its roots include α⁰ = 1 in addition to consecutive powers.

## Divisibility Structure

```
g_C₁(x) = g_C(x) × h₁(x)   where h₁ = [2, 2, 0, 1] (degree 3)
g_C₂(x) = g_C(x) × h₂(x)   where h₂ = [2, 1] (degree 1)
```

h₂ = [2, 1] represents x + 2 = x − 1 (mod 3), the minimal polynomial of α⁰ = 1.

h₁ corresponds to the minimal polynomials of the extra roots {α¹⁴, α¹⁶, α²²} needed for designed distance 17.

## Intersection

```
g_{C₁∩C₂}(x) = g_C(x) × h₁(x) × h₂(x) = g_C(x) × h_inter(x)
```

where h_inter = h₁ × h₂ = [1, 0, 2, 2, 1] (degree 4).

This gives dim(C₁∩C₂) = 26 − (19+4) = 3, confirming the dimension ladder:

```
C₁∩C₂: dim 3
C₁:    dim 4 = (C₁∩C₂) + 1
C₂:    dim 6 = (C₁∩C₂) + 3
C:     dim 7 = C₂ + 1 = C₁ + 3
```
