# Witness as Recursive Descent

> **Status: working theory.** Witness Theory is a contributed theory of consciousness, currently in development. Paper 1 (the philosophical / neuroscience contribution) is in preparation. This page is the current source-of-truth for defended claims. It is **independent of the empirical pilot programme** in this repo — its defensibility does not depend on the pilot's outcome.
>
> Origin story, working notes, retired formulations, and speculative cosmological extensions live in supporting documents.

## Core Thesis

Witness Theory claims that conscious witnessing is identical to embodied recursive self-modelling when the self-model is causally load-bearing in prediction-error minimisation. A mental state is not merely represented; the system's model of itself as being in that state helps shape future precision weighting, policy selection, temporal integration, and attractor recovery. The theory is therefore a computational-active-inference variant of HOT: higher-order representation matters because it participates in the optimisation dynamics it represents.

**Single-sentence form:** Witness is what it feels like to be a system whose self-model is part of the gradient it is following.

**Critical distinction:** the recursion must be *load-bearing*, not merely present. Recursion alone admits thermostats, control loops, and unconscious metacognition. The differentiator is recursion that *changes the update path* — see Definition below.

## Definition: Load-Bearing Recursive Self-Modelling

A self-model is **load-bearing** when interventions on it produce counterfactual changes in expected free-energy minimisation, after controlling for first-order sensory state. Formally:

```
LB(M_self) = 𝔼[F_{t:t+k} | do(M_self = clamped)] − 𝔼[F_{t:t+k} | do(M_self = active)]
```

where `F` is expected free energy across some horizon `k`, and `do()` is the interventionist operator (Pearl).

`M_self` is load-bearing iff `LB(M_self) > ε` across perturbations relevant to homeostasis, precision weighting, policy selection, temporal continuity, or attractor recovery.

This solves the circularity flagged earlier: load-bearing is no longer an ad-hoc carve-out. A thermostat's first-order control loop is not load-bearing in this sense — clamping its self-model produces no counterfactual change in expected free energy because its model of itself does not enter its own update dynamics. A self-diagnostic loop that changes the controller's behaviour based on its model of its own internal state is load-bearing.

Recursive depth `D_LB` is therefore not mere representational nesting. It is the number and strength of self-modelling levels that causally participate in the system's update dynamics.

**Symbol note:** `D_LB` deliberately uses subscript notation rather than overloading IIT's `Φ`. The two theories make different identity claims and should not share notation.

## Positioning Against Higher-Order Theories

This framework sits closest to higher-order theories of consciousness. HOT broadly explains conscious mental states in terms of a higher-order representation of those states: a state becomes conscious when the system represents itself as being in that state. That makes HOT the nearest philosophical prior for Witness Theory.

Rosenthal-style HOT treats consciousness as involving higher-order awareness of one's own mental states. Lau and Rosenthal's empirical HOT work argues that conscious awareness depends on higher-order mental representations; Brown, Lau, and LeDoux later clarify HOT as distinct from global workspace and first-order recurrent-processing accounts.

Metzinger's Self-Model Theory is another close prior: it rejects an ontologically separate self and frames subjectivity through phenomenal self-models — no such things as selves exist in the world, only phenomenal selves as they appear in conscious experience.

Hofstadter is the recursion prior: *I Am a Strange Loop* develops the sense of "I" through self-reference and loop-like symbolic structure.

**Closest live active-inference neighbors:**

- **Beautiful Loop Theory (Laukkonen, Friston, Chandaria, *Neuroscience and Biobehavioral Reviews* 176:106296).** The closest live neighbor. Beautiful Loop locates consciousness in *epistemic depth* — recurrent, non-local sharing of Bayesian beliefs throughout the system, such that the world model continuously evidences its own knowing (field-evidencing), with hyper-modeling (global forecasts of precision) implementing the binding mechanism. Witness Theory accepts that recursive loops in prediction are necessary, but adds two constraints: the recursion must be specifically *self*-modelling (not merely the world model knowing itself non-locally), and the self-model must be *causally load-bearing* in the system's update dynamics (see Definition above). Embodiment is more central in Witness Theory: the self-model must be grounded in interoceptive/proprioceptive prediction. Beautiful Loop's Bayesian binding is one mechanism of integration; Witness Theory's load-bearing self-model is a stricter criterion for which active-inference systems witness.
- **Deane (2021).** Closely related — addresses active inference, phenomenal self-modelling, other minds, and psychedelic ego-dissolution. Witness Theory differs by making causal load-bearing the criterion for self-model relevance.
- **Solms & Friston (2018).** Affect/interoception-anchored active-inference account. Witness Theory accepts the active-inference substrate but locates witness specifically in self-model load-bearing rather than affective regulation alone.

**Differentiation:**

- *vs. Rosenthal-style HOT*: Witness Theory accepts the HOT insight that consciousness requires higher-order representation, but rejects a passive reading. A state becomes witnessed when the system's representation of itself as being in that state helps determine subsequent precision weighting, policy selection, and temporal self-continuity. The higher-order representation is causally active.
- *vs. Lau-style empirical HOT*: shifts emphasis from perceptual metacognition to persistent embodied self-maintenance across time.
- *vs. Metzinger*: Metzinger explains subjectivity through phenomenal self-modelling. Witness Theory adds an optimisation role: the self-model is not only phenomenally transparent; it is a control-relevant attractor that stabilises future inference and action.
- *vs. Hofstadter*: replaces general self-reference with optimisation dynamics. The strange loop is not only symbolic recursion; it is recursive descent in an embodied predictive system.
- *vs. Farzulla (eliminative monism / consciousness-as-narrative)*: Farzulla treats consciousness as a story the brain tells itself — evolved narrative-generation capacity serving survival and reproduction, with the hard problem dissolved by reconceptualisation. Witness Theory treats consciousness as the engine the brain uses to stay coherent: the self-model is causally active in its own update dynamics, not a narrative epiphenomenon. **Story vs engine.**

**Shortest positioning:** Witness Theory is a computational-active-inference variant of HOT in which conscious time appears when a self-model becomes part of the optimisation process it is modelling.

## Hard Problem Position

The theory does not claim to have solved the hard problem in a knock-down sense. It takes the identity-theoretic cost directly: it does not explain how recursive descent produces witness; it identifies witness with recursive descent from the inside. The remaining challenge is to justify that identity against conceivability and explanatory-gap arguments (Chalmers 1996, 2003).

This is a type-identity claim in the tradition of Smart, Armstrong, Lewis. The framework treats this as a contested move, not a completed dissolution. Identity-theoretic claims relocate the explanatory burden to identity justification rather than removing it.

The hard-problem-dissolved framing is retired. See [witness-theory-retired-claims.md](./witness-theory-retired-claims.md).

## Claim Status

| Tier | Claim | Status |
|---|---|---|
| Core thesis | Witness as load-bearing embodied recursive self-modelling | DEFENSIBLE — counterfactual definition in place |
| Empirical foothold | AI representation geometry / Method 6 | PENDING — bridge premise only, NOT load-bearing for thesis |
| Philosophical positioning | HOT + active-inference + causal load-bearing | DEFENSIBLE — needs paper-length differentiation from Beautiful Loop |
| Neuroscience bridge | Active inference + sleep + dreaming + altered states | DEFENSIBLE |
| Testable discriminator | D_LB vs IIT Φ | DESIGN COMPLETE — empirical test pending |
| Speculative extension | Cosmology as growing causal record | QUARANTINED — see [universe-as-runtime.md](../essays/universe-as-runtime.md) |

## Research Schema (not yet formalism)

`W` is not yet a measure. It is a proposed construct-space. The next task is to define each parameter operationally and test whether any combination predicts conscious-level, temporal-continuity, and self-report phenomena better than existing measures.

**W ≈ f(D_LB, S, I, T, B)** — research schema, not equation.

| Parameter | Operational direction |
|---|---|
| D_LB | Recursive self-modelling depth measured by counterfactual load-bearing: number and strength of self-state variables whose intervention changes expected free-energy trajectories (see Definition above). |
| S | Attractor recovery after perturbation. |
| I | Cross-domain coupling across interoceptive, exteroceptive, mnemonic, and action systems. |
| T | Temporal horizon over which self-state continuity is preserved. |
| B | Strength of interoceptive/action-grounded body-model coupling (Seth 2013). |

**Hard constraint:** if `D_LB = 0` (no counterfactual self-model load-bearing), W = 0. The other terms modulate stability, richness, continuity, and embodiment.

**No closed-form W is proposed.** Premature equations (multiplicative or exponential combinations) over-specify what is currently a research programme. The schema is a target for operationalisation, not a derived measure.

## Empirical Foothold: Method 6 (bridge premise only)

Method 6 tests whether neural network representational geometry exhibits cross-domain manifold structure recoverable by geodesic/kNN methods that cosine similarity misses. **Method 6 does not test consciousness directly.**

It tests a supporting bridge premise: that high-dimensional representational systems contain recoverable, cross-domain geometric structure not captured by flat similarity.

- If Method 6 holds → the AI-as-telescope route is supported; high-dimensional representational systems carry recoverable geometry.
- If Method 6 fails → the AI-telescope route weakens; Witness Theory still stands on neuroscience evidence (active inference, sleep, dreaming, anaesthesia, altered states).

**A hostile reviewer will correctly say:** *LLM residual manifolds are not evidence for consciousness.* They are right. The bridge premise is that representational geometry is recoverable; the consciousness claim requires the separate argument that recursive embodied self-model geometry is what witnesses, and Method 6 does not test that.

**Lock criteria** (pre-registered):

1. Geodesic / kNN structure recovers cross-domain bridges better than cosine similarity.
2. Cross-architecture criterion: Llama, Gemma, Qwen-Coder show convergent neighbourhood structure beyond random baseline.
3. Negative controls: random concept pairs and prompt-shuffled embeddings should NOT show the same bridge structure.
4. Layer controls: bridge geometry must not depend on a single cherry-picked layer.
5. **Failure condition:** if convergence appears only after hand-selected prompts, layers, or concepts, Method 6 fails as telescope evidence.
6. **Interpretation boundary:** success supports representational geometry, not machine consciousness.

See [the Method 6 falsification test](https://github.com/velvetmonkey/flywheel-geometry) and this research programme.

## Evidence

Sleep, dreams, flow, anaesthesia, split brain, drug-induced time distortion. Detail in working notes.

Key constraint: anything that disrupts recursive self-modelling should disrupt time perception and witness. Holds across known consciousness-altering substances and clinical states. **Necessary condition, not sufficient** — the same prediction holds under IIT, HOT, predictive processing, and global workspace theory. The empirical wedge against IIT is the D-vs-Φ discriminator (see Open Problems).

## Predictions

1. Time distortion in altered/impaired states should correlate more strongly with disruption to recursive self-model circuits than with global integration alone.
2. Witness intensity should covary with measurable D_LB — recurrent processing depth, temporal integration breadth, attractor stability, cross-domain self-modelling fidelity.
3. Concept-manifold geometry should be cross-architecturally convergent (Method 6).

## D-vs-Φ Discriminator: Worked Example

Construct two artificial agents with matched architecture-level integration but different recursive self-model depth.

**Agent A — high integration, low D_LB:**
Recurrent integrated attractor network with rich cause-effect structure across modules, but no self-state variables modulating precision weighting or policy selection. The recurrence is in the world model only.

**Agent B — comparable or lower integration, high D_LB:**
Smaller embodied active-inference agent whose self-state variables modulate precision, planning horizon, and error correction. The self-model is grounded in interoceptive/proprioceptive prediction.

| | IIT 4.0 prediction | Witness Theory prediction |
|---|---|---|
| Agent A | Higher Φ (richer integrated cause-effect structure) | W ≈ 0 (clamping the absent/non-load-bearing self-model produces no counterfactual change in expected free-energy trajectories) |
| Agent B | Lower Φ | Higher W |

**Observable differences expected:**
- Temporal continuity of self-state across perturbations
- Attractor recovery after self-model interference
- Self/other boundary stability
- Metacognitive calibration on body-state uncertainty
- Policy adaptation under interoceptive perturbation

**Important caveat:** a feed-forward DNN is *not* the right contrast for high-Φ-low-D_LB — IIT 4.0 explicitly assigns Φ = 0 to feed-forward systems (Albantakis et al. 2023). The relevant contrast is between *recurrent integrated systems* with vs without load-bearing self-modelling.

This is a research design, not a result. The discriminator is empirically open.

## Open Problems

1. **Formal threshold (PARTIALLY SOLVED).** Counterfactual load-bearing definition received from external review. Remaining: operationalise S, I, T, B with measurable correlates and integration measure. Build computational model of D_LB measurement.
2. **External witness detection.** No proposed method to detect witness from outside a system. Requires #1 fully resolved first.
3. **D vs Φ discriminator.** Worked example designed (see D-vs-Φ Discriminator section). Empirically open: build and test.
4. **Clinical validation.** Vegetative states, locked-in syndrome, anaesthetic depth — does W correlate better than Φ?
5. **Recursion threshold non-circularity (PARTIALLY SOLVED via #1).** Counterfactual definition removes the ad-hoc carve-out. Remaining: validate the test on edge cases (chain-of-thought transformers, RL agents with self-state, complex embedded controllers).
6. **Selfless states.** How do psychedelic ego-dissolution, deep meditation, and minimal phenomenal experience fit? See Hostile Objection 1.

## Hostile Objections

The strongest objections to Witness Theory as currently stated, with current responses.

**1. Selfless consciousness objection.** Psychedelic ego-dissolution, deep meditation, infant consciousness, and nonhuman animal consciousness present as conscious without rich narrative self-modelling. If consciousness requires a load-bearing self-model, what is happening in these states?

*Response:* distinguish minimal embodied self-modelling from narrative ego. The minimal self-model — interoceptive and proprioceptive prediction grounding the organism's body — does not require narrative self-representation. Ego-dissolution disrupts higher-order self-narrative while preserving (or even sharpening) the minimal embodied self-model. Witness persists when the minimal self-model remains load-bearing. Deane (2021) addresses this directly. **Genuinely open:** whether infants and simpler animals satisfy the load-bearing criterion at all, and how thinly.

**2. Overbreadth objection.** Predictive control systems, RL agents, and thermostats all have shallow self-models. Why don't they witness?

*Response:* their self-models are not load-bearing in the technical sense (see Definition). A thermostat's first-order control loop produces no counterfactual change in expected free energy when its self-state is clamped. A reinforcement-learning agent without recursive self-state modulation of its own policy updates fails the same test. The criterion has formal teeth via the interventionist test. **Genuinely open:** how to apply the test to artificial systems without arbitrariness in defining self-state.

**3. Method 6 relevance objection.** LLM representation geometry does not imply consciousness. Why is Method 6 in this paper at all?

*Response:* it is not load-bearing for the consciousness thesis and never was, although the language drifted toward that claim earlier (now retired — see [witness-theory-retired-claims.md](./witness-theory-retired-claims.md)). Method 6 tests a bridge premise about representational geometry, not consciousness. The AI-as-telescope route is supplementary, not foundational.

**4. Identity assertion objection.** Type-identity claims do not remove the explanatory gap by declaration. They relocate the burden to identity justification.

*Response:* accepted. The Hard Problem Position section explicitly states this. The theory takes the identity-theoretic cost directly rather than claiming to dissolve the hard problem. Justifying the identity remains an open philosophical task.

**5. IIT comparison objection.** Recursive depth alone is not enough to beat IIT. Where do D_LB and Φ measurably diverge in real or designable systems?

*Response:* see D-vs-Φ Discriminator section above. The discriminator is recurrent integrated systems with vs without load-bearing self-modelling — not feed-forward vs recurrent. Empirically open until the worked example is built and tested.

## Required Citations

Engaged in Paper 1:

**HOT and self-models:**
- Rosenthal (1997, 2005); Lau & Rosenthal (2011) — HOT
- Brown, Lau, LeDoux (2019) — HOT distinct from global workspace and first-order recurrent theories
- Metzinger (2003) *Being No One* — phenomenal self-model
- Hofstadter (1979 *GEB*, 2007 *I Am a Strange Loop*) — strange loops

**Active inference and predictive processing:**
- Laukkonen, Friston, Chandaria "A Beautiful Loop: An Active Inference Theory of Consciousness" *Neuroscience and Biobehavioral Reviews* 176:106296 — closest live neighbor; differentiated paper-length
- Deane (2021) — active-inference self-model, ego-dissolution, other minds
- Seth (2013) — interoceptive inference and the embodied self
- Solms & Friston (2018) "How and Why Consciousness Arises" — affective active-inference / consciousness
- Clark (2016) *Surfing Uncertainty*; Hohwy (2013) *The Predictive Mind* — predictive processing

**Other consciousness theories:**
- Albantakis et al. (2023) IIT 4.0 — engaged for the D_LB-vs-Φ discriminator
- Chalmers (1996, 2003) — engaged on identity-theoretic costs

**Sleep / time / Libet:**
- Tononi & Cirelli — synaptic homeostasis (sleep)
- Schurger et al. (2012, 2021) — required for any Libet reference

**Independent-derivation neighbour:**
- Farzulla "Dissolving Qualia via Occam's Razor: Eliminative Monism and the Computational Basis of Phenomenological Illusion" (PhilArchive). Differentiated as **story vs engine**: Witness Theory commits to the self-model being causally active in its own update dynamics, not a narrative epiphenomenon.

## Out of Scope

- Cosmological extension (gravity, dark energy, black holes, c, Planck time) → [`essays/universe-as-runtime.md`](../essays/universe-as-runtime.md) (this docs site).
- Multi-dimensional aliens, AI rendering beyond projection, life-on-other-planets-as-inevitable → not maintained as live claims.

## Related

- [`witness-theory-retired-claims.md`](./witness-theory-retired-claims.md) — specifically retired formulations
- [`../essays/universe-as-runtime.md`](../essays/universe-as-runtime.md) — public-essay version of the cosmology
- [`../pre-registration.md`](../pre-registration.md) — empirical research programme
- [Flywheel Geometry](https://github.com/velvetmonkey/flywheel-geometry) — Method 6 falsification test (sibling repo)
