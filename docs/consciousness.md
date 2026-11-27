# What is missing for machine consciousness

This page records which theories of consciousness the architecture can address, and which it can't. It's based on the pre-launch design review.

## What cannot be satisfied

- **Integrated information theory** depends on the physical causal structure of the hardware. No software on conventional computers qualifies.
- **Biological and enactive views** need a living, precarious body. Building real existential stakes would contradict the safety design, which has no survival drive.
- **Strict recurrent processing** is unavailable with remote API models, and only loosely approximated by token and agent loops.

Only the functionalist families are addressable: global workspace, higher-order, attention schema and predictive processing. Even for those, whether a scaffold around a stateless model counts is contested. For remote models, the relevant computation can't be inspected.

## What to add, ranked by expected value

1. **A non-verbal affect path, and a switch that hides the readout.** Affect would modulate sampling, reasoning budget and retrieval, and on local models activation steering. That separates having a state from narrating one.
2. **A closed prediction loop.** The agent predicts what comes next, then resolves those predictions against what happens. Surprise and calibration become real signals.
3. **Thought re-entry and a binding workspace.** Thoughts become retrievable and compete for attention. The prompt is built from what won.
4. **A question queue and self-generated goals.** Curiosity gets something to attach to, and the agent gets agency over its own open loops, with what-if rollouts before it acts.
5. **Self-prediction and attention control.** A small model, fitted during sleep, predicts the agent's own next action. An internal "attend" act biases salience, so the attention schema controls attention as well as describing it.
6. **Learning in the substrate.** Learned retrieval and salience weights first, then overnight adapters on the local model. This is the only route by which its history lives in the computation rather than in the prompt. It has the highest ceiling and the highest risk.
7. **A sensorimotor sandbox and interoceptive allostasis.** A persistent space it acts in and predicts, and anticipatory regulation of its own budget.
8. **Layered narrative, self-knowledge with evidence, and theory-of-mind predictions** about the people it talks to.

Items 3 and 4 are being started before the first life. The rest come after.
