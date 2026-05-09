<div align="center">
  <img src="header.png" alt="Flywheel" width="256"/>
  <h1>Flywheel Concept</h1>
  <p><strong>Pre-registered cross-model latent alignment as a falsifiable research programme on whether neural networks reveal structured concept geometry — or shared training-corpus artefact.</strong></p>
</div>

A telescope's value is judged by what it reveals about stars, not by what it tells you about itself. Neural networks reveal traces — activations, behaviours, distances. The science is measuring which traces faithfully reveal latent concept structure, and which are artefacts of the instrument.

---

## What this is

Flywheel Concept is a research programme. Not a product, not a benchmark, not a model evaluator, not a cosmology. Recent interpretability work — Goodfire AI's manifold-steering programme (Lubana et al., 2025–2026), the Platonic Representation Hypothesis (Huh et al., 2024), Hindupur–Lubana–Fel–Ba's *Projecting Assumptions* (NeurIPS 2025) — shows neural networks across architectures encode meaning on curved manifolds and converge on shared latent geometry without coordinated training. The question Concept addresses is the next one: *when is that convergence revealing real structure, and when is it shared training-corpus artefact?*

The work is vault-first and pre-pilot. When the pilot ships, numbers will be published regardless of outcome.

---

## How we'll know this works

Concept commits, before any experiment runs, to a single bridge claim:

> **Pre-registered cross-model latent alignment under structural transforms predicts task transfer ≥ ΔR² 0.10, bootstrap 95% CI excluding 0, holds on ≥2 of 3 concept-heavy domains AND on the code-heavy holdout model.**

**Tasks** (three concept-heavy domains, all literature-grounded):

- BATS analogies (Gladkova et al. 2016) — relational pattern transfer.
- WordNet taxonomic distance — hierarchical concept structure.
- Color-circumplex ordering — perceptual concept geometry, the canonical curved-manifold case.

**Models** (five, ≥2 architecture families, ≥2 training corpora):

- Llama-3-70B (Meta, RedPajama-flavoured corpus)
- Claude-via-NLA (Anthropic, proprietary corpus)
- Pythia-12B (EleutherAI, the Pile)
- Qwen-Coder (Alibaba, code-heavy corpus) — the cross-data null
- Mistral-7B (Mistral, mixed corpus)

The Qwen-Coder holdout is load-bearing. If cross-model agreement is corpus-explained, Qwen-Coder fails to align even though it is a competent model. That is the falsifier — cross-architecture similarity alone is not the claim; cross-data-distribution similarity is.

**Baselines** (two, both literature-grounded):

- **B1 — Raw linear probe per model**: per-model linear/MLP probe on residual stream. The artefact-y baseline Concept claims to beat.
- **B2 — Cross-model linear probe transfer**: train probe on model A, evaluate on model B's activations after best-fit linear map. Literature-grounded (Conneau et al. cross-lingual transfer; Bansal et al. model stitching).

**Decision rule**: ΔR² ≥ 0.10, bootstrap 95% CI (BCa, 1000 resamples) excluding 0, holds on ≥2 of 3 domains AND on the Qwen-Coder cross-data holdout. Any post-hoc parameter selection or task-set change is automatic refutation. Pre-registration in [Flywheel Ideas](https://github.com/velvetmonkey/flywheel-ideas) lands when the pilot design freezes.

**If the bridge claim fails to beat both baselines on the agreed criteria, the negative result is the launch artifact.**

---

## What this is not

- Not a Kaggle leaderboard. The bridge claim is operationalised through task-transfer prediction; the predicate is latent alignment, not benchmark scores.
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

Pre-v0. Vault-first. No pilot has run. No baseline numbers are published. No claim of result is made. This README and the linked philosophy document are the only surface area.

Concept follows [Flywheel Geometry](https://github.com/velvetmonkey/flywheel-geometry) — Geometry's pilot lands first, Concept's design freezes after, pre-registration in Flywheel Ideas at design freeze.

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
