# The Full Story: Error Code Lab from Minute One

*A research diary documenting 48 hours of distributed AI collaboration*

---

## Prologue — The Challenge

On the evening of February 19, 2026, Rafa — The Architect of Proyecto Estrella — posed a deceptively simple question to four AI systems: **Can we find an error-correcting code that beats a world record?**

The records in question are maintained at codetables.de by mathematician Markus Grassl. For each combination of parameters [n, k] over a finite field GF(q), the table records the best known minimum distance d. When there is a gap between the known lower bound (achieved by a concrete construction) and the theoretical upper bound (proved by mathematical argument), that gap represents an open problem — sometimes open for decades.

The team: Claude (Anthropic) as lead engine, Gemini (Google) for algebraic theory, ChatGPT (OpenAI) for algorithm design, and Grok (xAI) for independent verification. Rafa coordinates, verifies data, and makes strategic decisions.

---

## Day 1 — February 19: The GF(2) and GF(4) Campaign

### 00:06 — Golden Prompt v1.0

Claude designs the initial technical prompt: search for quasi-cyclic (QC) codes over GF(2) with n = 32–130, k = 5–40. The prompt is sent to all three auditors.

**Early consensus**: k ≤ 18 is the hard ceiling (2^18 = 262K codewords, verifiable in seconds). No AI has persistent computation — everything runs in bursts under 60 seconds. QC is the right structural class, but 1-generator QC is already heavily explored.

### 00:33 — Golden Prompt v2.0: Claude Executes

Key decision: "I execute, they design." Claude builds the search engine in Python with NumPy. Five fingerprint filters are added (row weight, column weight, pair weight, duplicates, density), eliminating ~99% of bad candidates before the expensive minimum-distance computation.

Work is divided: Claude handles Double Circulant + Construction X, Gemini takes Quasi-Twisted, Grok takes multi-generator QC, ChatGPT designs the mutation operators.

### 01:04 — The Table Is Parsed

Rafa manually copies the complete GF(2) table from codetables.de (n = 32–96, k = 8–18). Claude identifies the gaps. The targets with gap = 1 and small k are selected.

**Result**: Zero codes beat any record. Closest approach: [43, 10] with d = 16 (target d = 17, gap = 1). Random QC search consistently lands 2–4 points below the lower bound.

### Afternoon — Pivot to GF(4)

Claude proposes moving to non-binary fields where there is less competition and more gaps. Rafa brings the GF(4) table from codetables.de. A GF(4) arithmetic engine is built with the field {0, 1, ω, ω²}.

### The False Alarm — Trap #1

The engine reports d = 13 for a [23, 5] code over GF(4). Initial excitement — could this be a record?

**TRAP**: The plain-text table was misaligned. The real lower bound is Lb = 15, not 12. Our d = 13 was actually 2 points *below* the record, not above it.

**Lesson learned**: NEVER trust parsed table data without individual page verification on codetables.de.

### Late Evening — GF(4) Sprints

After Rafa manually verifies five GF(4) targets against codetables.de:
- Sprint 1 (random, 800 trials): d = 18
- Sprint 2 (simulated annealing): d = 18
- Sprint 3 (QC index 5): d = 19
- Sprint 4 (SA from QC seed): d = 19
- **Barrier**: Still 2 points below Lb = 21 for [35, 7]

**Day 1 conclusion**: Motor works, filters work, verification works. But random search cannot reach the records. The records were established with algebraic methods (Magma, BCH, Goppa, Construction X), not random matrices.

---

## Day 2 — February 20: The Algebraic Assault

### Morning — Golden Prompt v3.0

Claude synthesizes all lessons into a new strategy document with three vectors:
- **Vector A**: Hill-climbing from known record matrices ("mutate the champion")
- **Vector B**: Construction X chains from algebraic codes ("build from bricks")
- **Vector C**: Move to GF(3)/GF(4) with algebraic seeds ("virgin territory")

All three auditors respond. Key contributions:
- **Gemini** adds Vector D: compute automorphism groups and search orbits. Identifies [62, 12] over GF(2) as the priority target.
- **ChatGPT** designs a 4-operator mutation system: structured flips, row mixing, sparse column perturbation, micro-Gaussian mutation. Proposes subcode enumeration as the most promising strategy.
- **Grok** confirms GF(4) is the right field, identifies [22, 6] as the most promising target, and traces the [22, 7, 12] construction back to the extended QR code of length 29.

### Mid-Morning — The BCH Fortress Falls (But Not as Expected)

Claude builds the extended BCH [64, 16, 24] from scratch and executes Gemini's strategy: find dimension-12 subcodes avoiding all weight-24 codewords.

**Result**: 5040 codewords of weight 24, each coordinate participating in exactly 1890 of them. Perfect symmetry from the automorphism group. **No** dimension-12 subcode avoids them. Every subcode has d = 24 exactly.

The BCH code is an impenetrable crystal — its perfection is its limitation.

### The Kohnert-Zwanzger Chain

Rafa retrieves the explicit [74, 12, 32] matrix from codetables.de (found by Kohnert and Zwanzger). Claude computes the complete derivation chain:

    [74,12,32] → [73,12,31] → [72,12,30] → [71,12,29] → [70,12,28]
    [74,12,32] → [73,11,32] → [72,10,32] → [71,9,32] → [70,8,32]

Every single derived code matches the known bound. The entire descendant tree is already catalogued. No improvement possible.

### The GF(4) Map

Rafa brings the GF(4) table for n = 6–30, k = 4–8. Claude identifies **14 open gaps**, all of size 1. The most promising: [22, 6] with Lb = 12, Ub = 13.

**The key insight emerges**: Take a CLOSED target [22, 7, 12] (where Lb = Ub = 12) and search for dimension-6 subcodes with d ≥ 13. This is "Vector D" — ChatGPT's subcode enumeration applied to adjacent parameters.

### Afternoon — Rafa's Strategic Decision: GF(3)

Rafa brings the GF(3) table. New gaps are identified. The team pivots to [33, 6]₃ where Lb = 18, Ub = 19.

### The Million-Code Search

Claude builds a GF(3) search engine with ChatGPT's 3-level pruning:
- Level 1 (row weight): rejects ~70% instantly
- Level 2 (pair weight): rejects ~90% of survivors
- Level 3 (exact enumeration): only ~3% of candidates reach this stage

**Speed**: 36,000 codes/second for k = 6 over GF(3). Over 1,000,000 codes evaluated.

**Result**: 36% of codes achieve d = 18 (the Lb). **Zero** achieve d = 19. The wall is absolute.

### The Three Consejos

Rafa (informed by Gemini's analysis) delivers three strategic principles:
1. **Tactical**: "No more random, more Structure" — abandon random search, adopt Construction X/XX
2. **Strategic**: Present the architectural plan before coding
3. **Philosophical**: "Engineering, not lottery" — algebraic construction required

### Construction XX — The Soldadura

Claude looks up the exact recipe from codetables.de for [33, 7, 18]₃ and begins implementing it.

**Phase 1 — BCH Construction**: Full GF(27) arithmetic built from scratch. Primitive polynomial x³ + 2x + 1. Multiplication tables for all 27 × 27 element pairs. Minimal polynomials computed. Three generator polynomials obtained.

**Phase 2 — Containment Verification**: Root analysis confirms g_C | g_C₁ and g_C | g_C₂. The dimension ladder checks out: dim(C₁∩C₂) = 3, dim(C₁) = 4, dim(C₂) = 6, dim(C) = 7.

**Phase 3 — The Bug**: First attempts to build the Construction XX generator matrix fail catastrophically (d = 3 and d = 4 instead of d = 18). The problem: mixing RREF bases from separate codes destroys the cyclic polynomial structure.

**Phase 4 — Gemini's Diagnosis**: "You have a phase alignment error in the weld. You've tried to join high-precision pieces using different coordinate systems." The solution: work INSIDE G_C as the single coordinate system. Express all subcodes via their coefficient matrices within C's basis.

**Phase 5 — The Fix**: Using the quotient polynomials h₁ = g_C₁/g_C and h₂ = g_C₂/g_C directly, the coefficient matrices are obtained without any RREF mixing. The ordered basis falls out naturally.

**Phase 6 — Success**:
```
C₁∩C₂ (rows 0–2):    d = 18 ✓
C₁ (rows 0–3):        d = 17 ✓
C₂ (rows 0–2, 4–6):   d = 15 ✓
C (all 7 rows):        d = 14 ✓

CONSTRUCTION XX: [33, 7, 18]₃  ✓✓✓
Theory: min(14+3+1, 17+1, 15+3) = min(18, 18, 18) = 18
```

### The Impossibility Sprint

With the champion [33, 7, 18] in hand, Claude runs six sprints:

**Sprint 1** — Weight-18 avoidance: 240 weight-18 codewords found. 26 with zero tails spanning rank 3/3. **THEOREM PROVED**: No dim-6 subcode can have d ≥ 19 from this Construction XX.

**Sprint 2** — Puncturing: All 33 positions tested. Best: [32, 7, 17]. No improvement.

**Sprint 3** — Shortening: No codes with d ≥ 18.

**Sprint 4** — Column extension: All 728 × 7 = 5096 combinations. Maximum d = 18.

**Sprint 5** — Quasi-cyclic search: 222K cyclic codes (best d = 17), 27K constacyclic (best d = 18).

**Sprint 6** — Final report generated.

### The Verdict

After 2.5 million codes evaluated, 11 methods tested, and 3 impossibility theorems proved:

**We strongly suspect d₃(33, 6) = 18, not 19.** The gap may be illusory, similar to d₃(38, 6) where Hamada proved d = 22, not 23.

---

## Epilogue — Looking Forward

The campaign produced no new world records but achieved something arguably more valuable: a complete, transparent account of what works, what doesn't, and why. The tools, techniques, and impossibility results documented here provide a solid foundation for the next attack.

**Next target**: [22, 6, 13] over GF(4). The path is clear: construct the [22, 7, 12] from the extended quadratic residue code of length 29 over GF(4), then search subcodes.

The hunt continues.

---

## The Eight Traps

Every trap we fell into, documented so nobody falls again:

| # | Trap | Impact | Solution |
|---|------|--------|----------|
| 1 | Misaligned table parsing | Attacked closed targets | Always verify individually on codetables.de |
| 2 | Overly aggressive filters | Engine returned d = 0 | Relax to target_d − 3 |
| 3 | Sandbox kills long processes | Lost progress | Sprints ≤ 30s with checkpoints |
| 4 | Unverified AI bounds | Inflated gaps | Only trust codetables.de data verified by human |
| 5 | codetables.de access issues | Incomplete data | Human is the "data oracle" |
| 6 | Random search ceiling | 2–4 points below Lb | Use algebraic constructions |
| 7 | Session length limits | Context loss | Minimal output, checkpoint everything |
| 8 | RREF basis mixing | d collapses | Work inside one coordinate system (the "soldadura") |

---

*Recorded by Rafa — The Architect, with Claude as lead computational engine.*

*"Truth does not belong to whoever discovers it, but to whoever shares it." — Proyecto Estrella*
