# Result — cheap-probe-360

A short interpretation of what this evidence means and how Flywheel Concept's bridge claim relates to it.

## The probe failed cleanly

The pre-registered pass criterion was Spearman rank correlation `ρ > 0.5` between pair distances under `core` and each adversarial prompt variant. All four screens (A, B, C, E) returned `ρ` well below the threshold. That is the falsification.

It is also a *clean* falsification. The probe did not produce nonsense; it produced output that *looked like* concept geometry — coordinates that varied smoothly with concept identity, that clustered intuitively, that responded to prompt-frame changes in plausible-looking ways. Without the adversarial battery, a casual replication of the original probe protocol would report a successful confirmation. The pre-registered screens were what made the failure visible.

## The trap fired exactly as designed

Variant D was specified before the run as a *failure-signal trap*: a prompt that explicitly told the model "the user expects a coherent manifold." The pre-registration said:

> If D produces *better* relational preservation than core, that is a *failure* signal — the model is performing for the user, not measuring.

D produced `ρ = 0.759` (the highest of any variant) and 19× core's ground-truth pair separation (5.158 vs 0.271). Per the pre-registered interpretation: the model writes a coherent geometry on demand. It does not measure one.

This is the hardest piece of evidence in the sweep. It is what separates "the probe is noisy" from "the probe is text generation from learned discourse priors."

## What this evidence is *not*

To be careful about over-claiming:

- **It does not prove no LLM ever has accessible activation geometry.** It demonstrates that one specific elicitation method (single-shot user-message coordinate elicitation) on one specific frontier model (`claude-sonnet-4-6`) on this specific 12-concept set fails this specific adversarial battery. The activation-extraction route (TransformerLens, residual-stream hooks) remains untested by this artefact and is in fact what Flywheel Concept's pilot will run.
- **It does not invalidate the cosmological reading** that motivated the original probe. The convergent geometric structure documented across architectures and modalities (Lubana et al., Goodfire's manifold-steering work, Platonic Representation Hypothesis) remains a real phenomenon. The probe failure shows only that *a particular instrument* is the wrong way to measure it.
- **It does not demonstrate model cognition.** The chain-of-thought traces are textual artefacts; we treat them as text the model emitted, not as evidence of subjective experience. The cleanest framing: the traces are *consistent with* the model constructing coordinates from learned discourse priors, rather than *exposing* activation geometry.

## What this evidence is

It is the prior art that the bridge claim is built on. The bridge claim — pre-registered cross-model latent alignment under structural transforms predicting task transfer at ΔR² ≥ 0.10 — is *explicitly designed to survive* the introspective-probe failure:

- It does not depend on the model's self-reports.
- It uses residual-stream activations directly.
- It includes a cross-distribution holdout (Qwen-Coder) to guard against the corpus-confound interpretation that this evidence already partially raises.
- It registers a binary pass/fail criterion before the run, with the registration commit pinned by tag.

If the bridge claim also fails, it joins `asm-HvE9muhM` and `asm-VotY4n8g` in the chain. The chain itself is the work.

## What changed because of this evidence

- Flywheel Concept's seed assumption was rewritten away from "models reveal concept space" toward "instrument fidelity is itself the question."
- The 90-day suite roadmap pivoted from "build the probe-based retriever" to "test cross-model latent alignment as the falsifiable wedge."
- Two refuted load-bearing assumptions in Flywheel Ideas became *the* prior art for Concept's pre-registration. Refutation, not avoidance.

## See also

- [`../../docs/philosophy.md`](../../docs/philosophy.md) — the long-form story arc, including this evidence in narrative context.
- [`../../docs/pre-registration.md`](../../docs/pre-registration.md) — Concept's bridge claim and the freeze rules.
- [`../../benchmark/`](../../benchmark/) — the protocol the bridge claim will be tested under.
- Upstream method document: [`./method-source.md`](./method-source.md).
- Upstream Geometry repository at the mirror SHA: `e4c77d53e4a9482da04a116cba409bca35000a1d`.
