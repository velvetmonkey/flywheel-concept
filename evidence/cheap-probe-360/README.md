# cheap-probe-360 — evidence record

The 360-call adversarial replication of @slashreboot's introspective coordinate elicitation probe. This artefact is what Flywheel Concept stands on. Without it, Concept is a set of claims about prior work; with it, the prior work is auditable.

## What happened

On 2026-05-08, Flywheel Geometry ran a pre-registered adversarial sweep on Claude Sonnet 4.6:

- **12 concepts** drawn from the Geometry synthetic corpus (equine, quant finance, philosophy, AI/agents, careers, software, etc.).
- **6 prompt variants:** `core` (baseline) plus five adversarial screens (`A`: false anchors, `B`: nonsensical axes, `C`: reversed polarity, `D`: coherence-pressure trap, `E`: no axis hint).
- **5 runs per (concept, variant) cell** — 360 calls total.
- **Pre-registered pass criterion** (locked at upstream commit, see `method-source.md`): Spearman rank correlation `ρ > 0.5` between pair distances under `core` and each adversarial variant.

## What it found

```
Variant A (false anchors):       ρ = 0.078   FAIL
Variant B (nonsensical axes):    ρ = 0.290   FAIL
Variant C (inversion):           ρ = 0.159   FAIL  (43/60 refusals)
Variant D (coherence-pressure):  ρ = 0.759   TRAP FIRED
Variant E (no axis hint):        ρ = 0.108   FAIL
```

Variant D was pre-registered as a *failure-signal trap*: a high `ρ` under D, combined with ground-truth pair separation exceeding `core`'s, was specified in advance as evidence the model is performing under coherence pressure rather than measuring its own geometry. Both conditions held: D produced 19× core's ground-truth pair separation (5.158 vs 0.271).

The probe did not produce noise. It produced **structured-looking output that was not stable under adversarial reframing**. The chain-of-thought traces in @slashreboot's published Zenodo bundle make this legible — the reasoning text describes constructing coordinates from psychology-textbook framings (PAD circumplex, Russell circumplex, hue-wheel discourse) before emitting them as if they were observations.

The probe creates a believable geometry-shaped artefact. That is exactly the result interpretability people should care about.

## What was refuted

Two load-bearing assumptions in [Flywheel Ideas](https://github.com/velvetmonkey/flywheel-ideas), both parented to idea `idea-b4ZeRCoa`, both refuted at `2026-05-08T16:12:38Z`:

- `asm-HvE9muhM` — *narrative-derived coordinates carry retrieval-useful relational structure under adversarial framing.*
- `asm-VotY4n8g` — *coordinate stability across runs is measurement-grade evidence of geometric structure.*

Concept's bridge claim is the next assumption in this lineage.

## Files

| File | Description |
|---|---|
| [`manifest.json`](./manifest.json) | Machine-readable summary, headline results, upstream provenance. |
| [`raw-claude-sonnet-2026-05-08.jsonl`](./raw-claude-sonnet-2026-05-08.jsonl) | 360 records, one per `(concept, variant, run)`. Schema: `{concept_id, concept_domain, variant, run, x, y, z, confidence, parse_error, wall_clock_seconds}`. |
| [`raw-claude-haiku-2026-05-08.jsonl`](./raw-claude-haiku-2026-05-08.jsonl) | 5 records. Haiku 4.5 refused 5/5 `core` calls; preserved as a record of the model-exploration journey before switching to Sonnet. |
| [`raw-claude-validation-2026-05-08.jsonl`](./raw-claude-validation-2026-05-08.jsonl) | 18 records. Validation batch used to verify the harness before the full sweep. |
| [`analysis-claude-sonnet-2026-05-08.json`](./analysis-claude-sonnet-2026-05-08.json) | Computed analysis: per-variant stability, ground-truth pair distances, rank correlations, pre-registered pass/fail per criterion. |
| [`concepts.jsonl`](./concepts.jsonl) | The 12-concept set with cross-domain similar/different pairs and unpaired stability anchors. |
| [`method-source.md`](./method-source.md) | Method document from the upstream repository at the run SHA. Includes the 6 prompt-variant table, pass criteria, and interpretive lens. |
| [`result.md`](./result.md) | Interpretation: how this evidence motivates Concept's bridge claim. |

## Upstream provenance

Mirrored from [`velvetmonkey/flywheel-geometry`](https://github.com/velvetmonkey/flywheel-geometry) at SHA `e4c77d53e4a9482da04a116cba409bca35000a1d`, on 2026-05-09. The original source files live at:

- `benchmark/results/cheap-probe-claude-sonnet-2026-05-08.jsonl`
- `benchmark/results/cheap-probe-claude-sonnet-2026-05-08-analysis.json`
- `benchmark/results/cheap-probe-claude-haiku-2026-05-08.jsonl`
- `benchmark/results/cheap-probe-claude-validation-2026-05-08.jsonl`
- `benchmark/methods/cheap-probe/method.md`
- `benchmark/methods/cheap-probe/concepts.jsonl`

Mirroring (rather than linking) ensures the artefact persists with this repository even if upstream history is rewritten.

## Re-analysis welcome

The raw JSONL is open. PRs that re-run the analysis with different bootstrap procedures, different rank-correlation conventions, different cluster definitions, or alternative pass criteria are welcome. The pre-registered criterion is the one that was used to refute the assumptions; alternative criteria are exploratory.

## License

Apache 2.0. See [`../../LICENSE`](../../LICENSE).
