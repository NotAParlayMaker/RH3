# GRH for Dirichlet L-functions, in Lean 4

Research artifact. Not maintained and not accepting contributions.

A Lean 4 proof of the Riemann Hypothesis and of the Generalized Riemann
Hypothesis for Dirichlet L-functions, built on Mathlib and using only the
axioms `propext`, `Classical.choice` and `Quot.sound`.

The proof is based on Levent Alpöge's, with Claude (https://alpo.ge/remark.pdf).
This repository is a shorter version, produced in collaboration with my
colleagues at Anthropic, and Claude.

## Two editions

- `grh/`: readable edition, about 300,000 lines. Start at `grh/GUIDE.md`.
- `grh-compact/`: the same five theorems, about 76,000 lines.

Each folder is its own Lake project with its own README.

## Build

Needs Lean v4.35.0 and Mathlib at commit 56a00585. In either folder:

    lake exe cache get
    lake build
    lake env lean scripts/PrintAxioms.lean

A build takes one to two hours on 12 cores with 24 GB of memory (about
85 minutes more if the Mathlib cache is missing).

## Continuous verification

`.github/workflows/verify.yml` checks the claims above on every push, for both editions:
it scans the sources for `sorry`, `axiom`, `native_decide` and similar escape hatches,
checks that `src/Statements.lean` imports only Mathlib, builds from scratch, requires each of
the five theorems to depend on exactly `propext`, `Classical.choice` and `Quot.sound`, checks
their types against `Statements.lean` and Mathlib's `RiemannHypothesis`, and replays `Main`
through `leanchecker`. The full `grh` edition may exceed a hosted runner's 6-hour limit.

## Status

The proof has passed machine checks only, listed in each folder's README.
No mathematician has read it through, and no paper comes with it.

## License

Apache 2.0, Copyright 2026 Anthropic, PBC. See `LICENSE`, and `NOTICE` and
`ATTRIBUTION.md` in each folder.
