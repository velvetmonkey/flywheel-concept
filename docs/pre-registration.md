# Pre-Registration

```
Status:               DRAFT
Frozen at commit:     <pending>
Frozen date:          <pending>
Allowed changes:      typo fixes, broken-link fixes, clarifications
                      that do not change the empirical claim
Forbidden changes:    bridge-claim wording, decision rule, metric
                      definition, model panel, task list, baseline
                      definitions, bootstrap procedure
```

## What this document is

This is the live pre-registration record for Flywheel Concept's bridge claim. It moves from `DRAFT` to `FROZEN` at a tagged commit (target tag: `v0.1-prereg-frozen`) when:

1. The user has reviewed the bridge-claim wording and accepted it verbatim.
2. The four-item checklist in the vault gate spec (`tech/flywheel/flywheel-concept-falsification-gate.md`) is signed off.
3. The bridge claim is registered as an assumption in [Flywheel Ideas](https://github.com/velvetmonkey/flywheel-ideas), parented to the same lineage as `asm-HvE9muhM` and `asm-VotY4n8g`.
4. No pilot runs have been started.

After freeze, this document becomes immutable in substance. Edits that change the empirical claim, the decision rule, or the experimental design are automatic refutation under the rule below.

## The bridge claim (verbatim, draft)

> **Pre-registered cross-model latent alignment under structural transforms predicts task transfer with incremental coefficient of determination ΔR² ≥ 0.10, bootstrap 95% CI excluding 0, holding on ≥2 of 3 task domains AND on the code-heavy holdout model.**

## Pre-registration components

The full pre-registered design lives in four files. Together they constitute the protocol that freezes:

| File | Scope |
|---|---|
| [`../benchmark/models.md`](../benchmark/models.md) | Five-model panel: family, training distribution, activation-extraction layer, runtime budget. |
| [`../benchmark/tasks.md`](../benchmark/tasks.md) | Three task domains, with explicit subset rules (BATS semantic only), ground-truth structures, and exclusion criteria. |
| [`../benchmark/metrics.md`](../benchmark/metrics.md) | Precise ΔR² definition, regression specification, bootstrap procedure, unit of analysis, decision rule. |
| [`../benchmark/protocol.md`](../benchmark/protocol.md) | Experimental procedure: activation extraction, alignment fitting, task-transfer scoring, ordering and analysis pipeline. |

A change to any of those four files between the freeze tag and the pilot run is an automatic refutation event, even if the change is "obviously correct." The discipline only works if it cannot be revised under pressure.

## Refutation rule (binding once frozen)

The bridge claim is refuted under any of these conditions:

1. ΔR² < 0.10 over both B1 and B2 baselines on more than one task domain.
2. Bootstrap 95% CI of ΔR² (BCa, 1000 resamples, clustered) includes 0 on ≥2 domains.
3. Qwen-Coder cross-distribution holdout fails on all three domains, where Llama / Gemma / Pythia / Mistral pass.
4. Any post-hoc parameter selection, task substitution, model substitution, layer change, or metric change made after the freeze tag, even if the post-hoc change improves results.
5. Failure to publish results within the announced window (positive, negative, or null), where "results" means the analysis JSON, the per-cell results files, and the interpretation `result.md`.

Refutation is not failure. Refutation is what the falsifier was for. The negative result publication is the launch artifact, per inherited [Flywheel Geometry](https://github.com/velvetmonkey/flywheel-geometry) discipline.

## Allowed post-freeze changes

The following do not constitute refutation events:

- Typo fixes in any pre-registration document.
- Broken-link or path fixes.
- Clarifications that do not change the empirical claim, decision rule, metric, model panel, task list, or baseline definitions.
- Adding ablation analyses *after* the primary analysis is complete and reported, clearly labelled as exploratory.
- New baselines submitted via PR after the pilot, scored under the same protocol.

When in doubt: add to a new section labelled "Post-hoc" or "Exploratory." Do not edit the primary protocol.

## Freeze procedure

1. User reviews the four pre-registration component files plus this document.
2. User signs off explicitly on the bridge-claim wording, decision rule, model panel, task list.
3. The bridge claim is registered as an Ideas assumption (lineage: `idea-b4ZeRCoa` or successor).
4. A commit is made to this repository updating only this document — the `Status:` line moves to `FROZEN`, the `Frozen at commit:` line gets the parent commit's SHA, and the `Frozen date:` line gets the calendar date.
5. The freeze commit is tagged `v0.1-prereg-frozen` and pushed.
6. Public announcement (if any) cites the freeze tag.

Until step 5, no pilot run begins.

## Provenance

This pre-registration document inherits its discipline from the [Flywheel Geometry council resolution of 2026-05-07](https://github.com/velvetmonkey/flywheel-geometry) and from the two refuted load-bearing assumptions on [Flywheel Ideas](https://github.com/velvetmonkey/flywheel-ideas) that constitute Concept's prior art (`asm-HvE9muhM`, `asm-VotY4n8g`, both parented to `idea-b4ZeRCoa`, refuted 2026-05-08). Evidence for those refutations lives at [`../evidence/cheap-probe-360/`](../evidence/cheap-probe-360/).
