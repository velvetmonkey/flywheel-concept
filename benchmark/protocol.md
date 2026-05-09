# Protocol

The end-to-end experimental procedure for the v0.1 pilot. This document, together with [`models.md`](./models.md), [`tasks.md`](./tasks.md), and [`metrics.md`](./metrics.md), constitutes the freezable pre-registration. See [`../docs/pre-registration.md`](../docs/pre-registration.md) for the freeze rules.

## Overview

```
1. Load model + tokenizer.
2. For each concept item in each task domain:
   2.1 Construct prompt from the held-constant template.
   2.2 Forward pass; capture residual-stream activation at the
       pre-registered layer for each model.
   2.3 Aggregate token activations to a single vector per concept.
   2.4 Persist to disk.
3. For each (source model, target model) pair, on a fitting subset:
   3.1 Fit structural transform T_A→B (orthogonal Procrustes + linear).
   3.2 Hold out a test set of concept items.
4. For each task domain × (source, target) pair:
   4.1 Compute alignment scores on test items.
   4.2 Compute baseline scores B1 (per-model probe) and B2
       (cross-model probe transfer).
   4.3 Fit nested OLS regressions; compute ΔR².
   4.4 Compute clustered bootstrap CI (1000 BCa resamples).
5. Aggregate to domain-level and Qwen-Coder-subpanel level.
6. Report. Result is the launch artifact regardless of outcome.
```

## Prompt template

The prompt for activation extraction is held constant across all five models, all three tasks, all concept items. No system prompt. No instruction-following framing. The template is the bare concept term, optionally with a minimal context disambiguator from the task source.

```
<concept_term>
```

Or, where disambiguation is needed (BATS only, for polysemous terms):

```
<concept_term> (<short disambiguator from BATS source>)
```

For sentence-context tasks like WordNet pair distance, we use a Cloze template:

```
The relationship between <term_a> and <term_b> is...
```

The exact template per task is committed at protocol freeze under `corpus/templates.json`.

**No prompting tricks.** No few-shot examples. No instruction tuning prefixes. No "think step by step." The activation is extracted from the model's response to the bare concept, not from a coaxed introspection. This is a deliberate choice driven by the [evidence](../evidence/cheap-probe-360/) that introspective coordinate elicitation is text generation from learned discourse priors, not direct activation readout.

## Activation extraction

Per model, at the pre-registered layer (see [`models.md`](./models.md)):

1. Tokenize the prompt with the model's native tokenizer.
2. Forward pass with `output_hidden_states=True`.
3. Extract `hidden_states[L]` at layer L per model.
4. Aggregate to a single vector per concept:
   - If the concept term tokenizes to a single subword: take that token's activation.
   - Else: mean-pool the concept-token span.
   - For Cloze templates: take the activation at the `<term_a>` position only (the second term and the connective are not used in the alignment fit).
5. L2-normalise the per-concept vector.
6. Persist as `evidence/v0.1/{model}/{task}/{concept_id}.npz` with metadata.

No quantisation. No mixed precision below FP16. Activations are extracted in BF16 where the model was trained in BF16, FP16 otherwise; converted to FP32 for analysis.

## Alignment fitting

For each ordered (source, target) model pair (A, B):

1. **Fitting set:** 70% of concept items per task, drawn at random with a seed registered at protocol freeze. The same fitting set is used for all 20 ordered pairs.
2. **Transform family:** orthogonal Procrustes followed by an optional learned diagonal scaling, no nonlinearities.
   - Procrustes: T_orth = argmin_{T ∈ O(d)} ‖T · activation_A − activation_B‖_F over the fitting set.
   - Optional diagonal scaling: D = argmin_{D diagonal} ‖D · T_orth · activation_A − activation_B‖_F.
   - Final transform: T = D · T_orth.
3. **No backprop.** No iterative gradient-based training. This is a closed-form alignment, deliberately limited to prevent the alignment from overfitting to the task signal.

The choice of orthogonal Procrustes (rather than a free linear map or a neural network) is a registered methodological commitment. A free linear map can absorb arbitrary signal and would not constitute "alignment under structural transforms" in any meaningful sense. The orthogonality constraint is the structural transform.

## Test-set scoring

For the held-out 30%:

1. Compute alignment score X for each concept (residual fit quality of T at that concept).
2. Compute Y per task (see [`metrics.md`](./metrics.md)).
3. Compute B1 (per-model probe trained on the 70% fitting set, evaluated on the 30%).
4. Compute B2 (cross-model probe transfer with the same training/eval split).
5. Fit the nested OLS regressions per cell.
6. Bootstrap (clustered, BCa, 1000 resamples).
7. Aggregate to domain level.

## Repository layout (post-pilot)

```
benchmark/
  models.md           # this document's neighbour
  tasks.md
  metrics.md
  protocol.md
  corpus/
    bats-semantic-pairs.jsonl     # frozen at v0.1-prereg-frozen
    wordnet-pairs.jsonl
    color-terms.jsonl
    templates.json
  results-v0.1/
    activations/
      {model}/{task}/{concept}.npz
    alignment/
      {source}-{target}.npz       # fitted T per pair
    cells/
      {task}-{source}-{target}.json     # per-cell ΔR², CIs
    analysis-v0.1.json            # primary aggregated results
    bootstrap-v0.1/               # raw bootstrap distributions
    result.md                     # interpretation, regardless of outcome
```

## Resource and runtime budget

Reiterating from [`models.md`](./models.md):

- ≤24 GPU-hours total panel × tasks runtime.
- ≤USD 100 budget cap.
- Budget exceeded ⇒ partial results reported, missing cells flagged, claim auto-refuted.

## Reproducibility commitments

- Random seeds registered at freeze: numpy, torch, dataset shuffling, fitting/test split.
- Model checkpoints pinned to specific Hugging Face revisions in `models.md` (added at freeze).
- Activation-extraction code released under Apache 2.0 in this repo.
- Bootstrap analysis code released under Apache 2.0 in this repo.
- Independent re-runs welcome via PR. Methods that submit alternative alignment-fitting algorithms (under the same Procrustes-class structural-transform constraint) are scored under the same protocol and added to the result table.

## Future directions (not part of v0.1)

Registered explicitly so they cannot be smuggled into v0.1 as post-hoc additions:

- Multilingual extension. Defer to v0.2+.
- Layer-sweep ablations. Defer to v0.2+ as exploratory only; v0.1 commits to the middle-layer choice.
- Closed-frontier model comparison via NLA. Defer to v0.2+ pending public availability.
- Rotator-tier intervention experiments (geodesic steering on the alignment-defined manifold). Defer to v0.3+. Concept is Tier 1 (instrument fidelity); rotator is Tier 3.
- Goodfire-style behaviour-space alignment (vs activation-space). Defer to v0.2+.
- SAE-decoded concepts as the alignment targets (per Hindupur–Lubana–Fel–Ba). Defer to v0.2+.

## What this protocol does not promise

- Does not promise that activation alignment is the right level of abstraction for "concept geometry." It promises only to test whether *this specific operationalisation* of cross-model latent alignment predicts task transfer better than the registered baselines.
- Does not promise model-pair coverage of any specific architecture pair we don't list.
- Does not promise that null results are uninformative — null results are the launch.
- Does not promise that this is the right protocol. It promises that *this is the protocol we registered before we ran it*. The register-then-run discipline is the only thing being defended here; the design itself can and should be criticised post-result.
