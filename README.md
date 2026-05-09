<div align="center">
  <img src="header.png" alt="Flywheel" width="256"/>
  <h1>Flywheel Concept</h1>
  <p><strong>A falsifiable study of whether cross-model activations reveal structured concept geometry — or shared training-corpus artefact.</strong></p>
</div>

> **Status: draft pre-registration. No pilot run yet.** Protocol lives at [`docs/pre-registration.md`](./docs/pre-registration.md) and freezes at a tagged commit before the pilot runs.

A telescope's value is judged by what it reveals about stars, not by what it tells you about itself. Neural networks reveal traces — activations, behaviours, distances. The science is measuring which traces faithfully reveal latent concept structure, and which are artefacts of the instrument.

---

## What this is

Flywheel Concept is a research programme. Not a product, not a benchmark, not a model evaluator, not a cosmology. Recent interpretability work — Goodfire AI's manifold-steering programme (Lubana et al., 2025–2026), the Platonic Representation Hypothesis (Huh et al., 2024), Hindupur–Lubana–Fel–Ba's *Projecting Assumptions* (NeurIPS 2025) — shows neural networks across architectures encode meaning on curved manifolds and converge on shared latent geometry without coordinated training. The question Concept addresses is the next one: *when is that convergence revealing real structure, and when is it shared training-corpus artefact?*

The work is vault-first and pre-pilot. When the pilot ships, numbers will be published regardless of outcome.

---

## How we'll know this works

Concept commits, before any experiment runs, to a single bridge claim:

> **Pre-registered cross-model latent alignment under structural transforms predicts task transfer with incremental coefficient of determination ΔR² ≥ 0.10, bootstrap 95% CI excluding 0, holding on ≥2 of 3 task domains AND on the code-heavy holdout model.**

Full metric definitions, bootstrap procedure, and unit-of-analysis discussion live in [`benchmark/metrics.md`](./benchmark/metrics.md). Protocol freeze rules in [`docs/pre-registration.md`](./docs/pre-registration.md).

**Tasks** (three relational-structure domains, all literature-grounded — full scope in [`benchmark/tasks.md`](./benchmark/tasks.md)):

- **BATS semantic subsets** (Gladkova et al. 2016) — relational linguistic structure. Lexicographic + encyclopedic subsets only; inflectional and derivational morphology subsets excluded as token-level rather than concept-level.
- **WordNet taxonomic distance** — hierarchical concept structure.
- **Color-circumplex ordering** — perceptual concept geometry, the canonical curved-manifold case.

**Models** (five open-weight models, ≥2 model families, ≥2 training distributions — full table in [`benchmark/models.md`](./benchmark/models.md)):

- Llama 3.1 8B (Meta, RedPajama-style corpus)
- Gemma 2 9B (Google, proprietary public-corpus mix)
- Pythia 12B (EleutherAI, the Pile)
- Qwen 2.5 Coder 7B (Alibaba, code-heavy corpus) — cross-distribution stress test
- Mistral 7B (Mistral, mixed corpus)

The Qwen-Coder run is a **cross-distribution stress holdout**, not an independently decisive falsifier. A code-heavy model still has substantial natural-language pretraining (documentation, comments, package names, tutorials), so alignment success does not prove cross-corpus concept geometry, and alignment failure does not prove the effect is corpus artefact (could be tokenization, scale, post-training, layer choice, or task mismatch). Outcome is diagnostic and feeds the interpretation; it is not on its own the gate.

**Baselines** (two, both literature-grounded):

- **B1 — Raw per-model probe**: per-model linear/MLP probe on residual stream. The artefact-y baseline Concept claims to beat.
- **B2 — Cross-model linear probe transfer**: train probe on model A, evaluate on model B's activations after a best-fit linear map. Literature-grounded (Conneau et al. cross-lingual transfer; Bansal et al. model stitching).

**Decision rule** (precise version in [`benchmark/metrics.md`](./benchmark/metrics.md)): ΔR² ≥ 0.10 over both B1 and B2, bootstrap 95% CI (BCa, 1000 resamples, clustered by concept-item / relation-group / model-pair) excluding 0, on ≥2 of 3 domains AND on the Qwen-Coder cross-distribution holdout. Any post-hoc parameter selection or task-set change after the protocol-freeze tag is automatic refutation. Pre-registration in [Flywheel Ideas](https://github.com/velvetmonkey/flywheel-ideas) lands when the protocol freezes.

**If the bridge claim fails to beat both baselines on the agreed criteria, the negative result is the launch artifact.**

---

## What this is not

- Not a leaderboard. The benchmark exists only to falsify the bridge claim. There is no ranking of models by score.
- Not the Universal Semantic Coordinate System. USCS is held in [docs/philosophy.md](./docs/philosophy.md) as the upper bound this work could become; the bridge claim is the necessary condition, not the conclusion.
- Not a finance product. No finance-domain experiments before the method is proven on cyclic time, scalar order, and concept-heavy taxonomies.
- Not a cosmological claim about reality. The cosmological reading lives in [docs/philosophy.md](./docs/philosophy.md), owned and linked, not on this front door.
- Not a rotator-tier claim. Rotator usefulness — can we move along the geometry, can behaviour follow geodesic interventions — is Tier 3 of the model-comparison ladder. Concept is Tier 1: instrument fidelity.

---

## How this slots in

Flywheel Concept is one of four sibling research and product threads:

- **[Flywheel Memory](https://github.com/velvetmonkey/flywheel-memory)** — local-first AI memory layer for Obsidian. Grounded retrieval, safe writes, knowledge-graph engine. Production.
- **[Flywheel Ideas](https://github.com/velvetmonkey/flywheel-ideas)** — local-first falsifiable decision ledger. The pre-registration target for Concept's bridge claim.
- **[Flywheel Geometry](https://github.com/velvetmonkey/flywheel-geometry)** — geodesic retrieval extension. The instrument-calibration lab; the discipline Concept inherits.
- **Flywheel Concept** *(this repo)* — research programme on whether language models reveal structured concept geometry.

Concept is umbrella to Geometry's research lane. Geometry's adversarial-screen discipline produced the falsified probe that motivated Concept. Concept does not replace Geometry; it is what Geometry's empirical floor was pointing at.

---

## Status

**Draft pre-registration. No pilot run yet.** This repo holds:

- The bridge claim, the task list, the model list, the baseline list, and the decision rule (above).
- The frozen protocol document at [`docs/pre-registration.md`](./docs/pre-registration.md). Currently `DRAFT` — moves to `FROZEN` at a tagged commit when the user signs off.
- The evidence record at [`evidence/cheap-probe-360/`](./evidence/cheap-probe-360/) — the failed introspective-probe sweep that motivated this programme. Mirrored from [`flywheel-geometry`](https://github.com/velvetmonkey/flywheel-geometry).
- No baseline numbers, no pilot results, no claim of empirical outcome.

Concept follows [Flywheel Geometry](https://github.com/velvetmonkey/flywheel-geometry) — Geometry's pilot lands first, Concept's protocol freezes after, pre-registration in Flywheel Ideas at protocol freeze.

---

## Evidence

The programme stands on one piece of preserved evidence at [`evidence/cheap-probe-360/`](./evidence/cheap-probe-360/): the 360-call adversarial sweep on @slashreboot's introspective coordinate elicitation probe (12 concepts × 6 prompt variants × 5 runs, against `claude-sonnet-4-6`, 2026-05-08). Pre-registered Spearman rank-correlation pass criterion `ρ > 0.5` between core and adversarial variants. **All four screens failed** (A: 0.078, B: 0.290, C: 0.159, E: 0.108). The pre-registered failure-signal trap (variant D, coherence-pressure framing) fired at ρ = 0.759 with 18× core's ground-truth pair separation. Two load-bearing assumptions in [Flywheel Ideas](https://github.com/velvetmonkey/flywheel-ideas) refuted: `asm-HvE9muhM` and `asm-VotY4n8g`, both parented to idea `idea-b4ZeRCoa`.

The bridge claim above is the next assumption in that lineage. The chain itself is the work.

---

## Credit & Collaboration

Concept exists because of work that is not Concept's:

- [Goodfire AI](https://goodfire.ai/) — Ekdeep Singh Lubana, Thomas Fel, [@GoodfireAI](https://x.com/GoodfireAI) — for the manifold-steering programme that established representation-and-behaviour geometry as evidence of structure in data.
- [@slashreboot](https://x.com/slashreboot) — Matthew — for publishing the introspective coordinate elicitation probe with full chain-of-thought traces, the data that made the falsification possible.
- Hindupur, Lubana, Fel & Ba — *Projecting Assumptions: The Duality Between Sparse Autoencoders and Concept Geometry* (NeurIPS 2025, [arXiv:2503.01822](https://arxiv.org/abs/2503.01822)) — for the instrument-fidelity framing.
- Anthropic NLA team — for the Natural Language Autoencoders publication that defined the cleanest available baseline for introspective decoding.
- BetaTomorrow / Deep Manifold — *Single Token Geometry 04* — for the framing of activations and behaviour as traces of boundary-conditioned neural computation, not the manifold itself.
- Huh, Cheung, Wang & Isola — for the [Platonic Representation Hypothesis](https://arxiv.org/abs/2405.07987).

Coauthorship on derivative academic work belongs upstream.

---

## Philosophy

The cosmological reading, the Universal Semantic Coordinate System reframe, and the four-piece suite headline are held in [docs/philosophy.md](./docs/philosophy.md). Owned, not hidden. Read it for the story so far. Read this README for what is being claimed and how it could be wrong.

---

## License

Apache 2.0. See [LICENSE](./LICENSE).
