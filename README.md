<!-- solve-problem:1b7f8333-306b-4b95-9955-fa9cad7f7171 -->
# Optimal PCP length

A [Tangle Solve problem](https://solve.tangle.tools/problems/1b7f8333-306b-4b95-9955-fa9cad7f7171).

## What is the problem?

A probabilistically checkable proof (PCP) for a language L is a randomized verifier V that reads q bits (or symbols from alphabet Σ) of a proof string π of length N, uses r random bits, and satisfies: (completeness) x ∈ L ⇒ ∃π accepted with probability 1; (soundness) x ∉ L ⇒ every π is rejected with probability ≥ 1−ε (typically ε ≤ 1/2, or gap amplification to constant gap).

The PCP theorem guarantees constant q and polynomial N for all of NP. The open problem: **achieve simultaneously optimal parameters** — constant query complexity q (ideally q = 2 or 3), constant alphabet (or binary), soundness error bounded away from 1/2 by a constant, and proof length N = n·polylog(n), i.e., *near-linear* in the NP witness length n, with small polylog exponent. The precise frontier question: for each q and alphabet size |Σ|, what is the minimum achievable N as a function of n and ε? Known constructions force tradeoffs between q, |Σ|, ε, and N; no construction is known with all parameters simultaneously at their conjectured optima (q = 2–3, |Σ| = 2, ε = 1/2, N = Õ(n)). A subtle ambiguity: "optimal length" may mean O(n) exactly, n·polylog(n), or n·(log n)^c for small c — the census and literature treat near-linear length as the target; a fully linear-length constant-query PCP is an even stronger open variant.

## Why does it matter?

PCP parameters are the bottleneck in hardness-of-approximation: every inapproximability factor for, e.g., MAX-3SAT, Vertex Cover, or CSPs flows through the parameters (query complexity, alphabet, length blowup) of the underlying PCP, and a tight 3-query PCP would pin down the exact approximation threshold of many problems (e.g., resolving the Håstad-style constant for MAX-3SAT variants). Short PCPs also matter practically for proof-size in delegation/argument systems and for the Efficiency (composition) of the PCP theorem itself. If the frontier stays open, we cannot certify optimal constants for most hardness-of-approximation results.

## What's already known?

- **Dinur (JACM 2007):** gap amplification via expander walks gives constant-query PCPs of polynomial length with a clean combinatorial proof; length blowup is polynomial but far from linear.
- **Dinur–Harsha (2013):** composition of low-error 2-query PCPs using *decodable PCPs* yields 2-query PCPs over constant alphabet with constant soundness gap and near-linear length — but the polylog exponent and the constants are poor, and the decodable-PCP machinery is intricate.
- **Classical tableau-based constructions** (Polishchuk–Spielman, Harsha–Safra, Ben-Sasson–Sudakov–Wigderson era, mid-1990s–2000s) achieve near-linear length for constant-query PCPs via arithmetic-circuit verification / low-degree tests; again with large polylog overheads.
- **Håstad (2001)** gives 3-query, optimal soundness (ε → 1/2 matches the algorithmic threshold) but with polynomial length.
- **Known lower bound obstacle:** proof length must satisfy N ≥ 2^r roughly (verifier reads only 2^r possible query tuples), so linear length limits randomness to O(log n); the constraint is not information-theoretically impossible.
- The gap: no construction achieves 2–3 queries, small alphabet, near-linear length, *and* optimal soundness simultaneously; the composition step (which gives short length) is what degrades parameters.

## What would count as solving it?

1. **Upper bound (main goal):** A PCP construction (or proof that one exists) for 3SAT with proof length N = n·polylog(n), q = O(1) queries over constant (ideally binary) alphabet, completeness 1, soundness ≤ 1/2, with an explicitly bounded polylog exponent. A referee accepts this given full parameter statement plus proof.
2. **Fully linear variant:** N = O(n) with constant q — the strongest form; even q = 2, |Σ| = O(1) at some constant soundness gap with N = O(n) would be major.
3. **Lower bound (matching):** Prove that near-linear length is impossible for, say, 2-query binary PCPs with soundness below some threshold — any superlinear length lower bound for constant-query PCPs would be groundbreaking (note: this is open and hard, since it implies circuit/KT-type lower bounds (verify)).
4. **Tradeoff resolution:** A tight characterization of the (q, |Σ|, ε, N) frontier for constant q.

## How to start

1. **Read Dinur (2007) first** to internalize gap amplification and expander-walk composition; then **Dinur–Harsha (arXiv:1206.6432), especially the composition section**, since composition is where length is won or lost.
2. Trace where the polylog blowup accumulates: typically the outer verifier's degree/arity forces recursive composition depth. Ask: can a single-level composition (or a decodable PCP with better rate) reduce depth to O(1)?
3. Study the Polishchuk–Spielman near-linear-length line (verify exact citation) — the alternative "arithmeticization" route to short PCPs; compare parameter losses with Dinur-style composition.
4. **Main obstacle:** composition requires inner PCPs whose length-vs-query tradeoff is itself suboptimal, and soundness amplification (parallel repetition / gap amplification) costs either queries or length. A useful first target: shave the polylog exponent for 2-query PCPs, a measurable sub-goal.

## Key references

- I. Dinur, "The PCP Theorem by Gap Amplification," JACM 54(3), 2007. Proves the PCP theorem combinatorially via iterated gap amplification on constraint graphs and expander walks; gives constant-query polynomial-length PCPs. (verify DOI: 10.1145/1236457.1236459)
- I. Dinur, P. Harsha, "Composition of Low-Error 2-Query PCPs Using Decodable PCPs," SIAM J. Computing 42(6), 2013; arXiv:1206.6432. https://arxiv.org/abs/1206.6432 — Builds decodable PCPs and uses them to compose 2-query PCPs achieving near-linear length with low error; the closest known result to the goal.
- J. Håstad, "Some Optimal Inapproximability Results," JACM 48, 2001. Constructs 3-query PCPs with optimal soundness 1/2+ε for MAX-3SAT-type problems, settling many hardness constants (at polynomial length). (verify)

## Warnings

- "Optimal" is ambiguous: optimal soundness (Håstad-style) vs. optimal length (near-linear) vs. both — always state which combination you target.
- Length lower bounds for PCPs are entangled with major open lower-bound questions; do not expect quick negative results.
- The Dinur–Harsha construction's constants and polylog exponent are large and the analysis is technical; re-deriving it is a multi-month effort — work incrementally on one composition parameter.
- A common dead end: naive parallel repetition to boost soundness blows up query complexity, undoing constant-query claims.

---
*`ALGO-000016` · flagged for review*

## Acceptance guidance

1. **Upper bound (main goal):** A PCP construction (or proof that one exists) for 3SAT with proof length N = n·polylog(n), q = O(1) queries over constant (ideally binary) alphabet, completeness 1, soundness ≤ 1/2, with an explicitly bounded polylog exponent. A referee accepts this given full parameter statement plus proof.
2. **Fully linear variant:** N = O(n) with constant q — the strongest form; even q = 2, |Σ| = O(1) at some constant soundness gap with N = O(n) would be major.
3. **Lower bound (matching):** Prove that near-linear length is impossible for, say, 2-query binary PCPs with soundness below some threshold — any superlinear length lower bound for constant-query PCPs would be groundbreaking (note: this is open and hard, since it implies circuit/KT-type lower bounds (verify)).
4. **Tradeoff resolution:** A tight characterization of the (q, |Σ|, ε, N) frontier for constant q.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/1b7f8333-306b-4b95-9955-fa9cad7f7171?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000016.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000016)
