<!-- solve-problem:a1f5da93-8c9c-4b8e-aae3-a9fe802c7ca8 -->
# Projection Games Conjecture

A [Tangle Solve problem](https://solve.tangle.tools/problems/a1f5da93-8c9c-4b8e-aae3-a9fe802c7ca8).

## What is the problem?

A **projection game** (equivalently, Label Cover) is a constraint satisfaction instance: a bipartite graph $G = ((X,Y), E)$, alphabets $\Sigma_X, \Sigma_Y$, and for each edge $e = (x,y)$ a constraint given by a function $\pi_e: \Sigma_X \to \Sigma_Y$. An assignment satisfies edge $e$ if $\pi_e(a(x)) = a(y)$; $\pi_e$ is a projection, so checking satisfiability is easy, but approximating the maximum satisfied fraction (the **value**) is hard. Write $\text{Opt}(I)$ for the optimum.

The **Projection Games Conjecture (PGC)** of Moshkovitz–Raz asserts: for every $\varepsilon > 0$ there is a polynomial-time reduction from any 3-SAT instance of size $n$ to a projection game $I$ of size $n^{1+o(1)} \cdot \text{poly}(1/\varepsilon)$ with alphabet size $\text{poly}(1/\varepsilon)$ such that:
- (completeness) if the 3-SAT instance is satisfiable, $\text{Opt}(I) = 1$;
- (soundness) otherwise $\text{Opt}(I) \le \varepsilon$.

The census record formulates the open task as: achieve **near-linear-size reductions to projection games with inverse-polynomial soundness** ($\varepsilon = 1/n^{\Omega(1)}$, or more precisely $1/\text{poly}(\text{size})$) while keeping alphabet $\text{poly}(1/\varepsilon)$ and size $N^{1+o(1)}$. The subtlety: "size" can mean input size $n$ or output game size $N$; the strongest reading demands soundness inverse-polynomial in $N$ with $N = n^{1+o(1)}$, which is the regime needed for tight set-cover hardness.

## Why does it matter?

The PGC is the conjectured "ultimate" PCP theorem: it would yield, essentially for free, tight NP-hardness of approximating set cover within $(1-\varepsilon)\ln n$ (via the Feige–Hastad–Klivans–Safra-style reduction from low-soundness projection games), plus optimal or near-optimal hardness for many label-cover-based problems (e.g., coloring, min-unsat, various covering problems). Current Raz verifier–based PCPs lose polynomial blowups or use super-constant repetitions to reach such low soundness, making reductions non-tight. Any construction of high-dimensional-expanders with stronger local-testability/soundness tradeoffs directly feeds both this conjecture and the agreement-testing literature.

## What's already known?

- **Moshkovitz–Raz (2008/2010)**: a parallel repetition theorem giving projection games with soundness $\varepsilon$ from size $N = n^{1+O(\varepsilon^{-1})}$ — a superpolynomial blowup as $\varepsilon \to 0$; this is the classical barrier.
- **Moshkovitz (2015,Theory of Computing)**: proves set cover hardness of $(1-\varepsilon)\ln n$ under the PGC and, unconditionally, hardness approaching $\ln n$ up to a slowly decaying additive gap via a careful composition; the paper also states and motivates the conjecture precisely.
- **Dinur–Harsha (2013)**: composition of PCPs with small soundness; a modular tool for building low-soundness verifiers, but not by itself near-linear size at inverse-polynomial soundness.
- **Bafna–Minzer–Vyas (arXiv:2407.12762; STOC 2025)**: building on high-dimensional expanders (Grassmann/HDX agreement tests), give PCP constructions reaching small **constant** soundness with near-linear size — the current state of the art per the census, but not inverse-polynomial soundness. The missing ingredient is an HDX/agreement-test analog of "superposed parallel repetition" achieving soundness $1/\text{poly}$ with alphabet $\text{poly}(1/\varepsilon)$.

## What would count as solving it?

A deterministic polynomial-time reduction $R$: $3\text{SAT}_n \mapsto$ projection game $I$ with $|I| \le n^{1+o(1)}\cdot\text{poly}(1/\varepsilon)$, $|\Sigma| \le \text{poly}(1/\varepsilon)$, completeness 1, soundness $\varepsilon$, **for all $\varepsilon \ge 1/n^{c}$ for some constant $c > 0$** (the inverse-polynomial regime), with a complete correctness proof. Intermediate milestones a referee would value: (a) any near-linear construction breaking below constant soundness (e.g., $\varepsilon = n^{-\Omega(1)}$ with size $n^{1+o(1)}$); (b) proving the PGC (constant-to-arbitrary $\varepsilon$ with size $n^{1+o(1)}$); (c) improved parallel-replacement lemmas on HDX (agreement theorems with $1/\text{poly}$ soundness and bounded alphabet). Under the construction, a corollary deriving NP-hardness of $(1-o(1))\ln n$ set-cover approximation would certify the reduction is in the useful regime.

## How to start

1. Read Moshkovitz (2015) Sections 1–3 for the exact conjecture statement, the set-cover reduction, and what parameters it needs.
2. Read Dinur–Harsha (2013) to understand PCP composition at low soundness — the standard route to pushing soundness down without repetition blowup.
3. Read Bafna–Minzer–Vyas (arXiv:2407.12762) carefully for the HDX/agreement-test verifier, and identify exactly where the soundness analysis caps out at a constant (typically the alphabet–soundness tension in agreement theorems on Grassmann graphs).
4. Try to generalize their "derandomized/superposed repetition" analysis: the main obstacle is that known HDX agreement tests have soundness limited by list sizes, and pushing soundness to $1/\text{poly}$ naively forces alphabet $\exp(1/\varepsilon)$ or size blowup $n^{O(\varepsilon^{-1})}$ (the Raz bound).

## Key references

- Dana Moshkovitz, "The Projection Games Conjecture and the NP-Hardness of ln n-Approximating Set-Cover," *Theory of Computing* 11(7), 2015. States the PGC formally; proves near-tight set-cover hardness assuming it and unconditionally up to slack. https://theoryofcomputing.org/articles/v011p007
- M. Bafna, D. Minzer, K. Vyas, "Constant Soundness PCPs with Near-Linear Size" (verify exact title), arXiv:2407.12762, DOI: 10.1145/3717823.3718197. Builds near-linear-size PCPs with small constant soundness via high-dimensional expanders and agreement testing.
- Irit Dinur, Prahladh Harsha, "Composition of Low-Error 2-Query PCPs using Decodable PCPs," *Theory of Computing* 9(15), 2013. Modular composition technique for low-soundness 2-query (projection) PCPs.
- Ran Raz, "A Parallel Repetition Theorem," *SIAM J. Computing* 27(3), 1998. The classical tool for soundness reduction, with the polynomial size blowup the PGC aims to avoid. (verify pagination)

## Warnings

- Ambiguity in the target: "inverse-polynomial soundness" may mean in the input size $n$ or output size $N$; the set-cover application needs the latter (or careful bookkeeping). Fix the parameterization before attempting anything.
- Alphabet size must stay $\text{poly}(1/\varepsilon)$; constructions with exponential alphabets are useless for the standard label-cover reductions.
- Naive parallel repetition is a dead end: it's exactly what the conjecture says can be avoided; any solution whose size analysis reproduces $n^{O(1/\varepsilon)}$ is not progress.
- Beware "soundness" conflations: agreement-test soundness (list-decoding), PCP soundness, and label-cover value are related but distinct quantities; HDX papers use their own conventions.
- The census record is secondary-source; verify all statements against the primary papers, especially the exact achievements of Bafna–Minzer–Vyas (marked "(verify)" above where unsure).

---
*`ALGO-000104` · unverified*

## Acceptance guidance

A deterministic polynomial-time reduction $R$: $3\text{SAT}_n \mapsto$ projection game $I$ with $|I| \le n^{1+o(1)}\cdot\text{poly}(1/\varepsilon)$, $|\Sigma| \le \text{poly}(1/\varepsilon)$, completeness 1, soundness $\varepsilon$, **for all $\varepsilon \ge 1/n^{c}$ for some constant $c > 0$** (the inverse-polynomial regime), with a complete correctness proof. Intermediate milestones a referee would value: (a) any near-linear construction breaking below constant soundness (e.g., $\varepsilon = n^{-\Omega(1)}$ with size $n^{1+o(1)}$); (b) proving the PGC (constant-to-arbitrary $\varepsilon$ with size $n^{1+o(1)}$); (c) improved parallel-replacement lemmas on HDX (agreement theorems with $1/\text{poly}$ soundness and bounded alphabet). Under the construction, a corollary deriving NP-hardness of $(1-o(1))\ln n$ set-cover approximation would certify the reduction is in the useful regime.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/a1f5da93-8c9c-4b8e-aae3-a9fe802c7ca8?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000104.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000104)
