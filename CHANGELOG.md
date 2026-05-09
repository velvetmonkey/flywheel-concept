# Changelog

All notable changes to Flywheel Concept will be recorded here. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [v0.2.0] — Draft pre-registration; protocol files; evidence record

### Added

- `docs/pre-registration.md` — the live pre-registration record. `Status: DRAFT`. Moves to `FROZEN` at a tagged commit when the user signs off on bridge-claim wording, model panel, task list, and decision rule. Includes the binding refutation rule and the freeze procedure.
- `benchmark/models.md` — five-model panel with family / training distribution / public-weights status / activation-extraction layer / runtime budget. Drops aspirational `Claude-via-NLA` from v0.1 (deferred pending public NLA availability); swaps in Gemma 2 9B. Adds Qwen 2.5 Coder 7B as the cross-distribution stress holdout with its diagnostic-not-decisive caveat.
- `benchmark/tasks.md` — three task domains. Restricts BATS to *semantic* subsets only (lexicographic + encyclopedic), excludes inflectional and derivational morphology subsets as token-level rather than concept-level. WordNet taxonomic distance with stratified 500-pair sample. Color circumplex with 11 basic colour terms.
- `benchmark/metrics.md` — precise ΔR² definition, regression specification (nested OLS), bootstrap procedure (1000 BCa resamples, *clustered* by category / root concept / model pair), unit of analysis (20 ordered model pairs), mixed-effects sanity check, edge-case pre-registration. Replaces the underspecified ΔR² in v0.1.0's README.
- `benchmark/protocol.md` — end-to-end experimental procedure: prompt template, activation extraction, alignment fitting (orthogonal Procrustes + optional learned diagonal scaling), test-set scoring, repository layout, compute and budget caps, reproducibility commitments, future-direction registry.
- `evidence/cheap-probe-360/` — the 360-call adversarial probe sweep that motivated the programme. Mirrored from `velvetmonkey/flywheel-geometry@e4c77d53e4a9482da04a116cba409bca35000a1d`. Includes raw JSONL (sonnet, haiku, validation), analysis JSON, concepts and method-source documents, machine-readable manifest, narrative `result.md`. Concept now stands on a preserved artefact, not a citation to another repo.

### Changed

- README subtitle reframed to a single-sentence falsifiable claim: *"A falsifiable study of whether cross-model activations reveal structured concept geometry — or shared training-corpus artefact."*
- README adds a `Status: draft pre-registration. No pilot run yet.` banner above the introduction.
- "Not a benchmark" reworded to "Not a leaderboard. The benchmark exists only to falsify the bridge claim."
- "≥2 architecture families" reworded to "≥2 model families and ≥2 training distributions" — the panel is decoder-only transformer LLMs throughout, distinguished by family / training mix / scale / post-training, not by radical architecture differences.
- Qwen-Coder framing: was load-bearing falsifier; now diagnostic, not independently decisive. Failure or success is one screen among several, with explicit caveats about tokenization, scale, post-training, layer choice, and task mismatch.
- Model panel: `Claude-via-NLA` removed from v0.1 (no public access surface for activation-grade NLA at this time); replaced with Gemma 2 9B. Llama-3-70B downsized to Llama 3.1 8B Instruct to match the rented-GPU budget cap.
- BATS framing: was "concept-heavy domain"; now "BATS semantic subsets" with explicit subset list and exclusion criteria.
- Bridge claim sentence expanded to spell out "incremental coefficient of determination" rather than the bare "ΔR²", with a pointer to `benchmark/metrics.md` for the precise definition.
- `docs/philosophy.md` removes the anthropomorphic phrase "models *consciously construct* coordinates" in favour of "the traces are consistent with the model constructing coordinates from learned discourse priors, rather than exposing activation geometry." Adds an explicit disclaimer that the chain-of-thought traces are textual artefacts and we make no claim about model cognition.
- `benchmark/README.md` rewritten as the index of the four pre-registration component documents, replacing the v0.1.0 placeholder.

### Inheritance

This release responds to external critique that v0.1.0 was a *research programme declaration* but not yet a *research artefact*. The repo now contains the failed-probe artefact, a frozen-on-tag protocol, exact metric definitions, and an exact model/layer/runtime plan. The result file lands when the pilot runs.

## [v0.1.0] — Initial release

### What this is

A research programme on whether neural networks reveal structured concept geometry, or whether observed cross-model agreement is shared training-corpus artefact. The work is vault-first and pre-pilot.

This release establishes the public surface area of the project before any empirical claim is made:

- `README.md` — the falsifier-first homepage. Names the bridge claim, the tasks, the models, the baselines, the decision rule. States explicitly that the negative result is the launch artifact if the claim fails.
- `docs/philosophy.md` — the story so far. The cosmological reading, the failed introspective probe that birthed Concept, the two refuted load-bearing assumptions (`asm-HvE9muhM` and `asm-VotY4n8g`), the reframe, the Universal Semantic Coordinate System as upper bound, the four-piece suite positioning. Held off the front door, owned not hidden.
- `benchmark/README.md` — placeholder for the falsification-gate experiment scaffolding.
- Apache 2.0 license. Suite-consistent header image.

### What this is not

- Not a pilot run. No baseline numbers are published. No claim of result is made.
- Not a benchmark. The bridge claim is operationalised through task-transfer prediction, but the predicate is latent alignment, not leaderboard ranking.
- Not the Universal Semantic Coordinate System protocol. USCS is the upper-bound vision held in `docs/philosophy.md`; the bridge claim is the necessary condition, not the conclusion.

### What's coming

- Pilot design freeze. Pre-registration of the bridge claim in [Flywheel Ideas](https://github.com/velvetmonkey/flywheel-ideas).
- Pilot run on the five-model × three-task × two-baseline grid named in the README.
- Public results regardless of outcome.

### Inheritance

Concept inherits the falsification discipline of [Flywheel Geometry](https://github.com/velvetmonkey/flywheel-geometry):

- One narrow falsifiable claim, named before any experiment.
- Two literature-grounded baselines.
- Cross-data null in the model list (Qwen-Coder, distinct corpus).
- Public-pivot commitment if the claim fails.
- Vocabulary discipline: the cosmological reading lives in `docs/philosophy.md`, not on the front door.

[v0.2.0]: https://github.com/velvetmonkey/flywheel-concept/releases/tag/v0.2.0
[v0.1.0]: https://github.com/velvetmonkey/flywheel-concept/releases/tag/v0.1.0
