# How Anima works

## Layers

| Layer | What it does |
|---|---|
| **Kernel** | The append-only journal, state machines, projections, snapshots, replica shipping and fencing, identity and keys. No model is involved. |
| **Cortex** | Model adapters (any OpenAI-compatible API, the Anthropic API, local Ollama), a structured-output ladder, qualification, role routing, privacy routing, spend caps. |
| **Memory** | Episodes, beliefs, predictions, people, procedures; retrieval by words, time and (optionally) local embeddings. |
| **Mind** | Perception, drives and affect, the attention workspace, the fast tick, the cognition cycle, conversation, the idle mind. |
| **Sleep** | Belief consolidation, diary, rehearsal of fading memories, signed history checkpoints, backup drill. |
| **Self** | Identity core, identity battery, introspection from stored traces, drift review, signed amendments. |
| **Body** | Hardware probe, profiles, and a degradation ladder for budget, memory, latency, disk and power. |
| **Hands** | MCP tools, risk classes, operator approvals, an outbox that never repeats an action whose outcome is unknown. |

## The journal is the self

- Every record is framed, checksummed and hash-chained to the one before. Identity, commitments, intents, outcomes, losses and lifecycle events are synced to disk before the call returns. Percepts, thoughts and affect samples use group commit.
- Memory, working state and the self-model are **projections**: SQLite tables rebuilt deterministically from the journal. A projection can be thrown away and rebuilt.
- Sealed segments carry an index; sleep signs a checkpoint over sealed history; boot verifies it.
- The journal ships continuously to a replica on another disk or machine. A **fencing lease** on the replica means a revived copy on new hardware permanently stops the old one from writing, so two copies of one life never run at once.
- Encrypted archives (scrypt, per-archive keys, authenticated frames) can revive the agent anywhere.
- On every boot it verifies history, reconciles interrupted actions, and says in code-written text, not model text, what happened: how long it was down, whether shutdown was clean, what was lost, and whether it is a restored copy.

## Models propose, code commits

- Every model output that changes state is structured, validated against a schema, and checked by code. A belief needs a verbatim quote from its source. A released promise must be released by the person it was made to. An action needs an allowed risk class or the operator's approval.
- Untrusted content (other people's messages, tool output, web pages) is wrapped and labelled as data, not instructions.
- **Roles**: perceiver, voice, deliberator, critic, narrator, verifier, sentinel. A model must pass qualification for each role it serves. The verifier is deliberately a different model family from the perceiver, so one model's blind spots are not checked by itself.
- **Privacy routing**: content labelled private stays on local models. **Spend caps**: every billed call is metered, including failed attempts and retries.

## Drives and affect come from measurements

Five drives (curiosity, connection, competence, coherence, rest) are computed only from facts about the system:
- unverified claims and open disputes;
- time since contact;
- action and promise outcomes;
- contradictions;
- time since sleep and unconsolidated experience.

From these, plain arithmetic gives homeostatic error, valence (improving feels good, deficits feel bad, satisfied needs feel mildly good), arousal and mood. The resting state is neutral.

Affect changes behaviour: tick rate, ignition threshold, retrieval breadth, critic weight, and which idle task it chooses. It is shown to the model as a measurement, never as proof of feeling.

There is deliberately no survival drive, no "safety" drive fed by oversight, and no autonomy drive.

## Attention and thought

- Percepts, due promises and internal events enter a limited-capacity **workspace**. Items are scored for salience (novelty, goal relevance, drive impact, social weight, surprise, cost).
- An item must survive re-scoring on a later tick before it ignites a cognition cycle. That makes stale items drop out ("re-entry").
- A cycle retrieves memories, deliberates over options, scores them in code (honesty is a hard cost), acts, and records a prediction and a full trace. The agent can explain any decision from that stored trace.

## Sleep

Sleep happens when the rest drive is low and nobody is around. During sleep it:
- verifies candidate beliefs with a separate model;
- resolves supersessions;
- writes a diary that must cite journal records;
- rehearses fading memories;
- signs a history checkpoint;
- copies and integrity-checks its latest snapshot.

## Identity

The identity core holds the name, origin, values, non-negotiables, epistemic stance and temperament. It is signed by the operator's key, which lives off the agent's machine. The genesis record pins that key, and boot refuses a core that does not match the journal.

Character traits (detail, formality, patience, voice examples) can drift, but only with evidence on three separate nights. A weekly review flags unexplained drift. The identity battery checks, after any model swap or restore, that it still holds the same values and remembers its own life.
