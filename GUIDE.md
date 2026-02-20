# A Guide for Everyone

## What Are We Doing? (No Math Required)

Imagine you need to send a message across a noisy phone line. Some words will get garbled. An **error-correcting code** is like adding extra "check words" so the receiver can detect and fix mistakes — even if part of the message gets corrupted.

Every modern technology uses these codes: your phone, Wi-Fi, Bluetooth, hard drives, satellite TV, QR codes, deep-space probes. Better codes mean faster downloads, more reliable storage, and signals that work at longer distances.

## The World Record Table

A mathematician named **Markus Grassl** maintains a database at [codetables.de](https://codetables.de) that lists the best known error-correcting codes for every combination of parameters. Think of it like a periodic table, but for codes.

Each code has three numbers: **[n, k, d]**

- **n** = total length of the encoded message (bigger = more overhead)
- **k** = amount of actual information carried (bigger = more efficient)
- **d** = minimum distance — how many errors can be detected/corrected (bigger = more robust)

For any given n and k, mathematicians want to find the **highest possible d**. When there's a gap between the best known code and the theoretical maximum, that gap represents an open problem.

## What We Did

Over 48 hours in February 2026, we assembled a team of **four AI systems** — Claude, Gemini, ChatGPT, and Grok — coordinated by a human architect (Rafa), to attack these open problems.

We tried **11 different strategies** and evaluated over **2.5 million candidate codes**. We worked across three different mathematical fields (GF(2), GF(3), GF(4) — think of these as different "alphabets" for writing codes).

## What We Found

### We Built Working Codes
We successfully constructed several codes from scratch using advanced mathematical techniques (BCH codes, projective geometry, Construction XX), proving we could reproduce the methods that experts use.

### We Proved Some Things Are Impossible
We mathematically demonstrated that certain approaches **cannot** produce better codes, no matter how long you search. This is actually a valuable scientific result — it tells future researchers not to waste time on those paths.

### We Confirmed That AI Can Do Real Research
The four AI systems played complementary roles: one designed algorithms, another provided algebraic theory, a third executed computations, and the fourth verified results. The human coordinator provided strategic vision and verified data against the reference database.

## Why Does It Matter?

1. **Practical impact**: Better codes mean more efficient communications for everyone
2. **Scientific value**: Each improved bound is a publishable result in coding theory
3. **Methodological innovation**: Using multiple AI systems in coordinated adversarial research is new
4. **Open problems**: Some gaps in the table have been open for 14+ years

## What's Next?

We are now targeting **[22, 6, 13] over GF(4)** — a code that would protect 6 symbols of information using 22 symbols total, with the ability to detect more errors than any currently known code with those parameters. The gap has been open since at least 2011.

## How You Can Help

- **Mathematicians**: Review our impossibility proofs and suggest alternative constructions
- **Programmers**: Our search engines are in Python — faster implementations (C, Rust, CUDA) would enable deeper searches
- **Curious minds**: Read the [full history](HISTORY.md) — it reads like a detective story

---

*Proyecto Estrella — "Build bridges, not walls."*
