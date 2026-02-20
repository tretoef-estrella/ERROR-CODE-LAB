# Weight-18 Avoidance Analysis

## Method

Given a code C = [n, k, d], we want to know if a dimension-(k−1) subcode can have d' > d.

### Step 1: Enumerate All Codewords

For small k (≤ 8 over GF(3), ≤ 7 over GF(4)), exhaustive enumeration of all q^k codewords is feasible.

### Step 2: Identify Minimum-Weight Codewords

Collect all codewords of weight exactly d. Store their **coefficient vectors** (the k-tuple that generates them from the basis rows).

### Step 3: Hyperplane Avoidance Check

A dimension-(k−1) subcode is ker(v) for some v ∈ GF(q)^k \ {0}. This subcode avoids codeword c iff v · c ≠ 0 (dot product over GF(q)).

**Question**: Does there exist v such that v · c ≠ 0 for ALL minimum-weight codewords?

### Step 4: Rank Analysis

If the minimum-weight coefficient vectors span all of GF(q)^k, then NO hyperplane can avoid them all (every linear form has a nontrivial kernel intersecting the span). This gives a **structural impossibility**.

If they span a proper subspace of dimension r < k, then hyperplanes not containing this subspace exist, and a d' > d subcode MAY exist.

## Application to [33, 7, 18]₃

- 240 weight-18 codewords found
- 26 have zero auxiliary tails (from C₁∩C₂ component)
- These 26 coefficient vectors, restricted to first 3 coordinates, have rank 3/3
- Therefore: impossible to avoid → no dim-6 subcode has d ≥ 19

## General Principle

This analysis is most powerful when the code has a structured decomposition (like Construction XX) where some minimum-weight codewords live in a small, identifiable subspace. The rank of that subspace determines whether avoidance is possible.
