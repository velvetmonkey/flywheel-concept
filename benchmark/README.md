# Telescope Fidelity Benchmark

The benchmark exists only to falsify the bridge claim in the [top-level README](../README.md#how-well-know-this-works). It is not a leaderboard.

## Documents (draft)

- [`models.md`](./models.md) — the five-model panel, with family / training distribution / activation-extraction notes.
- [`tasks.md`](./tasks.md) — the three task domains, with subset rules (BATS semantic only) and ground-truth structures.
- [`metrics.md`](./metrics.md) — the precise definition of ΔR², the bootstrap procedure, the unit of analysis, and the decision rule.
- [`protocol.md`](./protocol.md) — the experimental protocol (activation extraction, layer choice, alignment fitting, task-transfer scoring, runtime plan).

These four documents together constitute the draft pre-registration. The freeze rules and status banner live at [`../docs/pre-registration.md`](../docs/pre-registration.md).

## When the pilot runs

This directory will receive:

- `results-v0.1/` — one results file per (model × task × baseline / method) cell.
- `analysis-v0.1.json` — primary ΔR² values, bootstrap CIs, per-domain breakdowns.
- `result.md` — interpretation, regardless of outcome (positive / null / refuted).

Submit your method via PR. Independent baselines welcome. The bridge claim is the only thing being tested; the benchmark is the apparatus.

