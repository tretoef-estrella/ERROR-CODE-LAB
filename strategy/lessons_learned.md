# Lessons Learned: 8 Traps and How to Avoid Them

Documented during the Error Code Lab campaign, 19–20 February 2026.

## Trap 1: Misaligned Table Parsing

**What happened**: The GF(4) bounds table from codetables.de, copied as plain text, lost its column alignment. We read Lb = 12 for [23, 5] when the real value was Lb = 15.

**Impact**: Wasted compute attacking a closed gap. False excitement followed by harsh correction.

**Solution**: ALWAYS verify each target individually at `BKLC.php?q=Q&n=N&k=K`. Never trust bulk-copied tables. The human coordinator is the "data oracle."

## Trap 2: Overly Aggressive Filters

**What happened**: A row-weight filter (`min_row_weight < target_d`) rejected ALL matrices for high-d targets, returning d = 0.

**Impact**: False negatives — the engine appeared to find nothing when it was actually rejecting everything before checking.

**Solution**: Relax filters to `target_d - 3`. Better to waste time checking a few bad candidates than to miss all good ones.

## Trap 3: Sandbox Kills Long Processes

**What happened**: Search campaigns exceeding ~60 seconds were killed by the execution environment.

**Impact**: Lost progress, partial results, wasted context.

**Solution**: Sprint model — maximum 30 seconds per burst. Checkpoint at end of each sprint: best matrix, distance, seed, method. Resume from checkpoint.

## Trap 4: Unverified AI Bounds

**What happened**: Gemini provided bounds from cached training data (2024/2025) that didn't match codetables.de. ChatGPT couldn't access most codetables.de pages.

**Impact**: Targets with inflated gaps that appeared easier than reality.

**Solution**: Only trust bounds that a human has verified on codetables.de within the current session. AIs propose targets; the human confirms them.

## Trap 5: Random Search Cannot Reach Records

**What happened**: Random quasi-cyclic and systematic matrix search consistently landed 2–4 points below the known lower bound, across all fields and all targets.

**Impact**: Over 1 million wasted trials before accepting this pattern.

**Solution**: Records were established with algebraic methods (BCH, Goppa, Construction X/XX, projective geometry). Random search is useful for verification and reaching Lb, but never for exceeding it. Use algebraic constructions for the Lb → Ub jump.

## Trap 6: RREF Basis Mixing (The "Soldadura")

**What happened**: When building Construction XX, computing RREF independently for each subcode and then combining the bases destroyed the cyclic polynomial structure. Result: d = 3 instead of d = 18.

**Impact**: Multiple failed implementations before diagnosis.

**Solution**: Work inside a SINGLE coordinate system (the main code C's generator matrix). Express all subcodes via coefficient matrices derived from polynomial quotients. Never mix RREF outputs from different codes.

## Trap 7: Perfect Symmetry Blocks Local Improvement

**What happened**: The extended BCH [64, 16, 24] has perfect automorphism symmetry. Every coordinate participates equally in weight-24 codewords (exactly 1890 each). Strategic shortening, puncturing, or subcode selection all produce identical results.

**Impact**: Gemini's strategy of "avoid weight-24 codewords via smart subcode selection" was mathematically impossible.

**Solution**: Recognize when a code's automorphism group makes all local operations equivalent. Such codes are "fortresses" — their perfection is their limitation. Use them as ingredients, not as objects to deform.

## Trap 8: Exhausting a Champion's Descendant Tree

**What happened**: The Kohnert-Zwanzger [74, 12, 32] code produced a beautiful derivation chain, but every single derived code exactly matched the known bound in codetables.de.

**Impact**: Hours spent computing puncturings, shortenings, and subcodes that were already catalogued.

**Solution**: Before deriving from a known code, check if the resulting parameters already have Lb = Ub (closed). If yes, the derivation cannot improve anything. Only derive toward open gaps.

---

## Meta-Lesson

The overarching lesson: **the gap between Lb and Ub is not a search problem — it's a construction problem.** More compute and more random trials do not help. The +1 jump requires finding the right algebraic structure, and that structure is specific to each parameter set.

*"Engineering, not lottery."* — Rafa's Third Consejo
