# Telescope Fidelity Benchmark

Placeholder. Lives here to reserve the directory and the convention.

When the pilot runs, this directory will hold:

- The pre-registered task set (BATS analogies, WordNet taxonomic distance, color-circumplex ordering).
- The model list and activation-extraction protocol.
- The two literature-grounded baselines (B1: per-model linear probe; B2: cross-model linear probe transfer).
- The decision rule (ΔR² ≥ 0.10, bootstrap 95% CI excluding 0, holds on ≥2 of 3 domains AND on the Qwen-Coder cross-data holdout).
- The result file: `results-v0.1.json` — primary outcome and ablations.

Submit your method via PR. Independent baselines welcome. The bridge claim is in [the README](../README.md#how-well-know-this-works).
