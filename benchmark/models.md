# Models

Five open-weight models, ≥2 model families, ≥2 training distributions. Open-weight requirement is non-negotiable for v0.1: the bridge claim depends on residual-stream activation extraction, which requires either weights access or a trustworthy activation-decoding intermediary (e.g., Anthropic's Natural Language Autoencoders).

We defer closed-frontier models to a future v0.2+ comparison and rely on NLA-class methods if and when public access exists. v0.1 keeps the panel concrete and reproducible.

## Panel

| Model | Family | Training distribution | Public weights | Notes |
|---|---|---|---|---|
| Llama 3.1 8B Instruct | Llama 3 | RedPajama-flavoured (Common Crawl + arXiv + books + GitHub + Wikipedia) | Yes | Large open ecosystem; well-studied activations. |
| Gemma 2 9B Instruct | Gemma 2 | Proprietary public-corpus mix (web, code, math) | Yes | Different family from Llama; trained with knowledge distillation. |
| Pythia 12B | Pythia (GPT-NeoX) | The Pile (academic-leaning, deduplicated) | Yes | Most distinct family in the panel; suite includes intermediate checkpoints if needed. |
| Qwen 2.5 Coder 7B | Qwen 2.5 | Code-heavy (GitHub-dominant) plus general pretraining | Yes | **Cross-distribution stress holdout** — see below. |
| Mistral 7B Instruct v0.3 | Mistral | Mixed corpus, sliding-window attention | Yes | Sliding-window attention is the most distinct architectural choice in the panel. |

## Activation extraction

- Library: [TransformerLens](https://github.com/neelnanda-io/TransformerLens) where supported, otherwise direct `transformers` hooks.
- Layer choice (pre-registered): residual-stream activations at relative depth 0.5 — the middle layer of each model. Specifically:
  - Llama 3.1 8B: layer 16 of 32.
  - Gemma 2 9B: layer 21 of 42.
  - Pythia 12B: layer 18 of 36.
  - Qwen 2.5 Coder 7B: layer 14 of 28.
  - Mistral 7B v0.3: layer 16 of 32.
- Token aggregation: mean over the concept-token span; if the concept tokenizes to a single subword, we take that token's activation directly.
- Prompt template (held constant across models): minimal, no system prompt, no instruction tuning bias — see [`protocol.md`](./protocol.md) for the exact template.

The middle-layer choice is a methodological commitment registered before any results. Per Hindupur–Lubana–Fel–Ba (NeurIPS 2025), the choice of layer is itself an instrument decision; we lock it ex ante to prevent post-hoc tuning.

## Cross-distribution stress holdout: Qwen Coder

Qwen 2.5 Coder 7B is the cross-distribution stress test in the panel. Its training corpus is code-dominant (a stark mix difference from the other four panel members) but it retains substantial natural-language pretraining: documentation, code comments, package names, README files, StackOverflow snippets, tutorials, error messages, and general pretraining data.

This is **diagnostic, not independently decisive**:

- If Qwen-Coder aligns: the cross-model latent alignment is not corpus-distribution-explained at the level of *web-text vs not-web-text*. Note that this does not establish concept-space universality — it does establish that the alignment survives a substantial corpus distribution shift within the language modelling family.
- If Qwen-Coder fails to align: the alignment may be corpus-explained — but it could also be tokenization (BPE differences from a code-heavy vocabulary), scale (smaller than three of the four others), post-training (instruction-tuning differences), layer choice (middle-layer assumption may not transfer), or task mismatch (the concept-heavy tasks may be poorly served by a code-tuned model).
- Either outcome feeds the interpretation. Neither alone is the falsifier — the bridge claim's gate is the ΔR² rule across ≥2 of 3 domains AND on Qwen-Coder.

## Why this panel and not Claude / GPT-4o / others

The v0.1 design needs activation access. Closed-frontier APIs do not provide it. The only published bridge from frontier-API behaviour to activations is Anthropic's [Natural Language Autoencoders](https://transformer-circuits.pub/2026/nla/index.html), which is not generally available as a developer surface at the time of pre-registration. We defer Claude / GPT / Gemini comparisons to v0.2+ pending NLA availability or equivalent.

This is a real limitation. v0.1 measures the bridge claim on the open-weight subset of the model space; whether it generalises to closed frontier models is an explicit open question, registered here.

## Compute budget

- Activation extraction: rented GPU (A100 40GB sufficient for inference at 70B-and-below scales; 80GB preferred for headroom). One-shot inference per (concept, model) cell. No fine-tuning.
- Estimated runtime per model on the full task corpus: 30–120 minutes depending on size and task length.
- Total panel × tasks budget: ≤ 24 GPU-hours plus analysis-pipeline CPU time.
- Budget cap: USD 100. If the budget caps before all cells complete, partial results are reported with the missing cells marked, and the bridge claim is automatically refuted under "failure to complete the registered protocol."

## Substitution rule

Models in this panel may not be swapped between freeze and pilot. If a model becomes unavailable (model release withdrawn, weights access broken, etc.), the protocol is updated *and* the change is publicly logged in this document with a `## Substitution log` section, with the substitution date and commit, before the pilot proceeds. Substitution after pilot start is automatic refutation.
