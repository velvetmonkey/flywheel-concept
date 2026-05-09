# Tasks

Three relational-structure domains. All literature-grounded. The set is small by design: the bridge claim is one narrow falsifiable claim, not a benchmark.

Per the critique that motivated this document's existence: the BATS subset is restricted to *semantic* categories only. The full BATS dataset includes inflectional and derivational morphology subsets, which are token-level (or sub-word level) rather than concept-level. We exclude them.

## Task 1 — BATS semantic subsets

**Source.** Gladkova, Drozd & Matsuoka, *Analogy-based Detection of Morphological and Semantic Relations With Word Embeddings* (NAACL-HLT 2016 SRW). Dataset at [vecto.space/projects/BATS](https://vecto.space/projects/BATS/).

**What we use.**

- L01 Hypernyms (animals)
- L02 Hypernyms (miscellaneous)
- L03 Hyponyms (miscellaneous)
- L04 Meronyms (substance)
- L05 Meronyms (member)
- L06 Meronyms (part-whole)
- L07 Synonyms (intensity)
- L08 Synonyms (exact)
- L09 Antonyms (gradable)
- L10 Antonyms (binary)
- E01 Geographic (capital-country)
- E02 Geographic (country-language)
- E03 UK_City — county
- E04 Person — occupation
- E05 Animal — young
- E06 Animal — sound
- E07 Animal — shelter
- E08 Things — colour
- E09 Male — female
- E10 Person — affliction

**What we exclude.** I01–I10 (inflectional morphology) and D01–D10 (derivational morphology). These test sub-word and morphological generalisation, not concept geometry. Including them would conflate two different research questions.

**Caveat.** Per the [ACL Wiki BATS State-of-the-Art](https://aclweb.org/aclwiki/Bigger_analogy_test_set_(State_of_the_art)) entry, analogy performance is sensitive to the solving method and is best treated as characterising an embedding rather than evaluating it directly. We use BATS to define a *relational structure* signal — pair-distance prediction across the 20 semantic categories — not a single accuracy number.

**Task framing.** For each pair (a, b) in a category, we extract the residual-stream activation for `a` and `b` at the pre-registered layer, compute their alignment-method distance, and ask: does this distance predict whether the pair is from the same category vs a randomly-sampled cross-category pair? The bridge claim is that cross-model latent alignment improves this prediction over the per-model baseline (B1) and the cross-model probe transfer baseline (B2), in a way captured by ΔR² (see [`metrics.md`](./metrics.md)).

## Task 2 — WordNet taxonomic distance

**Source.** Princeton WordNet 3.1, [wordnet.princeton.edu](https://wordnet.princeton.edu/).

**What we use.** Hierarchical concept structure. For a sample of 500 concept pairs drawn from the noun hierarchy, the ground-truth signal is the path distance in the hypernym tree (Wu-Palmer similarity). The task: does cross-model latent alignment predict Wu-Palmer similarity better than the baselines?

**Sampling.** 500 pairs, stratified across 5 distance buckets (0–1, 1–2, 2–4, 4–8, 8+ steps in the hypernym tree). Sample drawn once at protocol-freeze time and committed to `corpus/wordnet-pairs.jsonl` before the pilot runs. The exact pairs become part of the freeze.

**Why this task.** Hierarchical structure is one of the cleanest documented manifold structures in language model representations (Lubana et al., Goodfire). Concept geometry, if it exists, should preserve hypernym distances across models that have all encountered the same hierarchical concept structure in their pretraining.

## Task 3 — Color circumplex ordering

**Source.** Ekman's foundational hue-circle work, replicated in many later studies. We use the 11 basic colour terms (Berlin & Kay, 1969): red, orange, yellow, green, blue, purple, pink, brown, black, white, grey.

**What we use.** The hue-wheel ordering: red → orange → yellow → green → blue → purple → red (wrapping). Plus the achromatic axis (black–grey–white) and the neutral term (brown, pink). The task: does cross-model latent alignment predict the circular ordering of the chromatic terms — specifically, does the implied 1D circular distance in alignment-space correlate with hue-wheel angle?

**Why this task.** Colour is the canonical curved-manifold case in interpretability research (Goodfire's manifold steering work uses hue circles as a key example). It is small (11 terms), well-studied, and admits a sharp ground-truth structure (a circle is a circle).

**Why this task is small.** Eleven concepts is a small N for bootstrapping. The colour task contributes the *circular topology* signal to the bridge claim's panel; we do not bootstrap each task separately. The metric definition in [`metrics.md`](./metrics.md) clusters bootstrap units across tasks for the joint bridge-claim test.

## Domain rule

The bridge claim must hold on **≥2 of these 3 domains** AND on the Qwen-Coder cross-distribution holdout. "Hold" means the ΔR² rule with bootstrap CI excluding 0, as defined in [`metrics.md`](./metrics.md).

A claim that survives only on, say, color-circumplex but fails on BATS and WordNet does not pass: the bridge claim is for *relational structure* across multiple kinds of concept geometry, not a single domain.

## Concept items: the freeze

At protocol freeze, the exact concept items from BATS, the exact 500 WordNet pairs, and the exact colour-term list are committed under `corpus/`. The freeze includes:

- `corpus/bats-semantic-pairs.jsonl` — all pairs we use, drawn from the 20 semantic BATS categories.
- `corpus/wordnet-pairs.jsonl` — the 500-pair stratified sample.
- `corpus/color-terms.jsonl` — the 11 basic colour terms with hue-wheel angle annotations.

Post-freeze item swaps are automatic refutation.

## What this task list is not

- Not "the only tasks Concept ever cares about." It is the v0.1 panel only.
- Not finance. Finance lives in v1+ if and only if the v0.1 bridge claim survives.
- Not synthetic / probing benchmarks (BIG-bench, MMLU, etc.). Those test capability; we are testing *latent alignment*, which is upstream.
- Not multilingual. v0.1 is English-only. Multilingual extension is registered as a future direction in [`protocol.md`](./protocol.md).
