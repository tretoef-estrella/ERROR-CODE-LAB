# GF(3) Arithmetic Reference

## The Field GF(3)

Elements: {0, 1, 2}

### Addition Table (mod 3)
```
+ | 0 1 2
---------
0 | 0 1 2
1 | 1 2 0
2 | 2 0 1
```

### Multiplication Table (mod 3)
```
× | 0 1 2
---------
0 | 0 0 0
1 | 0 1 2
2 | 0 2 1
```

### Additive Inverse
- −0 = 0, −1 = 2, −2 = 1

### Multiplicative Inverse
- 1⁻¹ = 1, 2⁻¹ = 2

## Extension Field GF(27) = GF(3³)

**Primitive polynomial**: p(x) = x³ + 2x + 1 (irreducible over GF(3))

**Elements**: Triples (a₀, a₁, a₂) ∈ GF(3)³, representing a₀ + a₁α + a₂α²

**Total**: 27 elements (including 0 = (0,0,0))

**Multiplication**: Polynomial multiplication modulo p(x), with coefficients reduced mod 3.

**Key reduction rule**: α³ = α + 1 (from x³ ≡ −2x − 1 ≡ x + 2 mod 3)

Wait: x³ + 2x + 1 = 0 → x³ = −2x − 1 = x + 2 (in GF(3)). So α³ = α + 2.

### Primitive Element Powers

α = (0, 1, 0) has order 26 = |GF(27)*|.

Selected powers (as GF(3)³ triples):
```
α⁰  = (1, 0, 0) = 1
α¹  = (0, 1, 0) = α
α²  = (0, 0, 1) = α²
α³  = (2, 1, 0) = α + 2
α¹³ = −1 = (2, 0, 0)   (since 26/2 = 13)
α²⁶ = α⁰ = (1, 0, 0)   (period)
```

## Polynomial Arithmetic over GF(3)

Polynomials have coefficients in GF(3). Standard operations:
- **Addition**: coefficient-wise addition mod 3
- **Multiplication**: convolution with coefficient reduction mod 3
- **Division**: polynomial long division with GF(3) arithmetic

### Generator Matrix from Generator Polynomial

For a cyclic code of length n with generator polynomial g(x) of degree n − k:

```
Row i of G = coefficients of x^i · g(x), for i = 0, 1, ..., k−1
```

Each row is a shift of g(x) padded with zeros to length n.
