# Belov Code Construction from PG(3, 3)

## Overview

The Belov [32, 4, 21]₃ code is constructed by selecting 32 specific points from the projective geometry PG(3, 3), which has 40 points total.

## The Simplex Code S(4, 3)

The Simplex code S(4, 3) = [40, 4, 27]₃ uses ALL 40 points of PG(3, 3) as columns. Each nonzero vector in GF(3)⁴ defines a point (up to scalar multiple), giving (3⁴ − 1)/(3 − 1) = 40 points. The minimum distance is 27 = 3³ (every codeword has the same weight).

## Point Removal Strategy

We remove 8 points forming two coordinate 2-planes:

**Plane 1**: {(a, b, 0, 0) : (a, b) ∈ GF(3)², not both zero} — 4 projective points
**Plane 2**: {(0, 0, c, d) : (c, d) ∈ GF(3)², not both zero} — 4 projective points

These 8 points are disjoint in PG(3, 3) (no overlap since the two pairs of coordinates don't mix).

## Result

Removing these 8 columns from the 40-column Simplex generator matrix gives a [32, 4, 21]₃ code.

The minimum distance drops from 27 to 21 because there exist hyperplanes in PG(3, 3) that pass through many of the remaining 32 points while avoiding the removed ones.

## Derived Code

Puncturing columns 31–32 from the [32, 4, 21] gives a [30, 4, 19]₃ code, which was intended as the "búnker" (strong inner code) for Construction X approaches.

## Historical Note

This construction follows Belov et al. (1974), who used projective geometry techniques to construct codes achieving the Varshamov-Griesmer bound.
