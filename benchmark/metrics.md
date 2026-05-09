# Metrics

The bridge claim:

> Pre-registered cross-model latent alignment under structural transforms predicts task transfer with incremental coefficient of determination ΔR² ≥ 0.10, bootstrap 95% CI excluding 0, holding on ≥2 of 3 task domains AND on the code-heavy holdout model.

This document defines what every italicised noun in that sentence resolves to.

## Variables

For each (task domain, source model, target model) cell, we compute the following:

- **Y — task transfer score.** A continuous outcome variable per concept item. Specifically:
  - **BATS**: per-pair, the pair-distance in the source model's activation space, evaluated against the target model's same-pair distance in *its* activation space. Higher = better preservation of relational structure across models.
  - **WordNet**: per-pair, the source model's pair-distance vs the Wu-Palmer ground-truth distance, scored as the negative absolute residual (closer to ground-truth = better).
  - **Color**: per-term, the implied circular-distance in alignment-space vs the hue-wheel ground-truth angle, scored similarly.
  - In all three cases, Y is a continuous score per concept item or pair; higher means the model's representation better preserves the ground-truth relational structure.

- **X — cross-model latent alignment score.** A scalar per (source model, target model, concept item) triple. Computed from the alignment method:
  - For each model pair (A, B), fit a structural transform T such that T(activation_A(concept)) ≈ activation_B(concept) over a held-out fitting set. (The transform family is pre-registered in [`protocol.md`](./protocol.md): orthogonal Procrustes plus an optional learned linear map, no nonlinearities.)
  - The alignment score for a concept under (A, B) is the residual fit quality of T at that concept (e.g., negative reconstruction error normalised by activation norm, so higher = better alignment).

- **B1 — per-model baseline.** A linear/MLP probe trained per model, predicting Y from the source model's activations alone, no cross-model information. The artefact-y baseline.

- **B2 — cross-model probe transfer.** A linear probe trained on source model A's activations to predict Y, then evaluated on target model B's activations after a best-fit linear map. Literature precedent: Conneau et al. (2018) cross-lingual word embedding alignment; Bansal et al. (2021) model stitching.

## Regression specification

For each task domain, we fit two nested OLS regressions per (source, target) model pair on held-out test items:

```
Baseline model:   Y_i = β_0 + β_B * baseline_score_i + ε_i
Alignment model:  Y_i = β_0 + β_B * baseline_score_i + β_A * alignment_score_i + ε_i
```

Where `baseline_score` is the better of B1 and B2 for that cell (the alignment claim must beat *both* baselines, so we take the harder of the two as the comparison).

**ΔR² = R²(alignment model) − R²(baseline model)**

This is incremental coefficient of determination — how much variance in Y is explained by adding the alignment score on top of the baseline score. We use R² rather than R̄² (adjusted) because the dimensionality difference is exactly 1; R̄² would correct for that but at small N introduces noise that the BCa bootstrap handles cleanly.

## Bootstrap procedure

- **Resamples:** 1000 BCa (bias-corrected and accelerated) bootstrap resamples per cell.
- **Resampling unit:** clustered. The cluster structure is:
  - For BATS: cluster by *category* (20 BATS semantic categories), since pairs within a category share inflectional/lexical patterns. Resample categories with replacement, then take all pairs from each resampled category.
  - For WordNet: cluster by *root concept* in the hypernym tree. The 500 pairs sample from many distinct roots; we resample roots with replacement.
  - For Color: 11 terms is too small to cluster cleanly; we use a leave-one-out / jackknife procedure instead of bootstrap, noting this as a v0.1 limitation in the result.
- **Confidence interval:** 95% BCa.
- **Decision rule per cell:** ΔR² ≥ 0.10 AND lower CI bound > 0.

The clustered bootstrap is non-negotiable. Per the critique that motivated this design pass: bootstrapping over individual concept items while treating model-pair structure as independent inflates confidence. Cluster by the unit of true independence in the data.

## Mixed-effects alternative

For each task we also fit a mixed-effects model with:

- Fixed effects: baseline score, alignment score.
- Random effects: random intercept by source-model and by target-model.
- Random slopes by model-pair where the data support it.

The mixed-effects ΔR² (computed as the difference in marginal R² between the two models) is reported alongside the OLS-bootstrap ΔR² as a robustness check. **The OLS-bootstrap ΔR² is the primary; the mixed-effects ΔR² is the sanity check.** Disagreement between the two by more than 0.05 absolute is flagged in the result as inconclusive for that cell.

## Unit of analysis: model pairs

With 5 models we have:

- 10 unordered model pairs (5 choose 2 = 10).
- 20 ordered (source, target) pairs (5 × 4 = 20, excluding identity).

We use **ordered pairs** for the primary analysis because alignment under structural transforms is direction-sensitive in general (T_A→B ≠ T_B→A in the orthogonal Procrustes case unless T is symmetric). This gives 20 (source, target) cells per task domain × 3 domains = 60 primary cells, plus 5 self-cells which are excluded.

The **per-model holdout** for Qwen-Coder treats Qwen as either source or target across all four other models (8 cells per task × 3 domains = 24 Qwen cells out of the 60 total).

## What "holding on ≥2 of 3 domains" means

For each task domain (BATS, WordNet, Color), we aggregate ΔR² across the 20 ordered (source, target) cells:

- Domain-level ΔR² = mean of cell ΔR² values, weighted by per-cell sample size.
- Domain-level CI = clustered bootstrap CI, where the cluster is the (source, target) pair plus the within-task cluster from above (a two-level nested bootstrap).

The bridge claim "holds on a domain" iff:

1. Domain-level ΔR² ≥ 0.10
2. Domain-level 95% CI lower bound > 0

The bridge claim "holds on Qwen-Coder" iff the same rule passes when restricted to the 8 cells where Qwen-Coder is source or target, on ≥2 of 3 domains.

The full bridge claim passes iff:

- It holds on ≥2 of 3 domains across the full 20-cell panel, **AND**
- It holds on Qwen-Coder (≥2 of 3 domains in the Qwen-only 8-cell subpanel).

Failure of either conjunct refutes the claim. Partial passes are *reported*, but they do not pass the gate.

## Pre-registration of edge cases

Some edge cases that get registered ex ante to prevent post-hoc rescue:

- **Negative ΔR² with CI excluding 0:** the alignment score *hurts* prediction. Reported clearly. Counts as refutation, not anomaly.
- **Cell with insufficient items for stable bootstrap (N < 30):** flagged as `bootstrap-unstable` and excluded from the domain-level aggregation. Listed in the result as excluded cells.
- **Outlier cells (Cook's distance > 4/N at the cell level):** reported but not removed; we follow the conservative pre-registration convention that outliers stay in unless their inclusion was an obvious data-collection error.
- **Disagreement between OLS-bootstrap and mixed-effects ΔR² by > 0.05:** that cell is marked inconclusive for the per-cell analysis but contributes to the domain-level aggregation with its OLS-bootstrap value.

## What is *not* the metric

To prevent misreading:

- ΔR² is not accuracy on a task. We are not building a classifier.
- ΔR² is not improvement over random. It is incremental over the better baseline.
- ΔR² is not Pearson correlation between alignment and Y. It is incremental variance explained in a regression with the baseline as a covariate.
- ΔR² is not the *only* metric we report. The full result set includes per-cell R² values, per-domain bootstrap distributions, per-model-pair ablations, and the mixed-effects sanity check. ΔR² is the *gate* metric for the bridge claim — the one binary pass/fail criterion.

## Provenance

The decision rule was set by the user verdict on the [Flywheel Concept council resolution](https://github.com/velvetmonkey/flywheel-concept/blob/main/docs/philosophy.md) (vault: `tech/flywheel/flywheel-concept-council-2026-05-09.md`) on 2026-05-09. The clustered-bootstrap and mixed-effects details were added in this document in response to external critique that the original ΔR² spec was under-defined.
