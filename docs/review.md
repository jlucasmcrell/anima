# Pre-launch review (2026-11-27)

Before the first long-running life was started, five independent read-only reviews were run with Claude Fable 5.2:
- durability and identity;
- models, tools and safety;
- cognition;
- every commit made by OpenAI Codex;
- a self-critique of Fable's own original design.

Reviewers reproduced defects with throwaway scripts where they could. About 80 findings came back. Each was checked against the code before being fixed, and each fix gets a regression test where practical.

## The most serious findings

| Area | Finding | Status |
|---|---|---|
| Durability | The hourly snapshot could deadlock against the journal's commit thread (lock-order inversion), freezing the agent within days. The supervisor would not have noticed. | Fixed; a hung core is now killed and restarted |
| Durability | An unreachable replica disk crashed boot, and at runtime wrote a synced record every second while it was away. | Fixed |
| Identity | A core re-signed with a substituted key booted normally, so anything able to write the home could rewrite the agent's values. | Fixed: the operator key is pinned in the journal |
| Identity | `genesis` silently overwrote an existing operator key. | Fixed |
| Privacy | A message marked private still reached cloud models on the next turn, through the attention workspace. Found by a new test. | Fixed: private records stay out of every cloud-bound prompt |
| Spend | Failed attempts, retries and repairs were never charged, so the daily cap could be exceeded unseen. After a capped day, cloud models stayed blocked until restart. | Fixed: every call is metered |
| Tools | Tool servers inherited every API key. Undrained stderr could hang them. Open-world "read" tools (web fetch) ran unapproved. | Fixed |
| Affect | The mood was negative by construction: a three-hour conversation in which everything succeeded scored as badly as ten days alone. | Fixed: neutral rest, with deficits not masked |
| Cognition | Curiosity was pinned at zero, and idle belief checks counted as sleep. One ambiguous claim jammed the idle mind. "Defer" was an unbounded model-call loop. | Fixed |
| Cognition | After two or three quiet days the agent forgot the conversation: history was found by scanning back a fixed number of records. | Fixed: kind index |
| Cognition | Commitments never closed. Disputed beliefs never resolved. A person's own update often could not replace their earlier statement. Different facts on one topic overwrote each other. | Fixed |
| Codex's work | A rollup failure aborted every later sleep. The signed-history check could be switched off by deleting one file. The drift flag could be silenced by the agent's narrator quoting a single character. The offline baseline numbers were constructed. | Fixed; the baseline claim is withdrawn |

## The design self-critique, in brief

- **Persistence of identity is not sentience.** "The self is the record" answers survival of hardware failure. It works against the consciousness goal, because the candidate subject on most computational theories is the model's forward pass, which this design treats as a swappable organ.
- **Labels are not mechanisms.** A list is not a global workspace unless it is a bottleneck that modules compete for. A model's stated confidence is not a higher-order representation. A self-report that paraphrases numbers placed in the prompt shows reading comprehension, not introspection.
- **Several loops were open.** Predictions never resolved, thoughts never re-entered attention, goals were never created, and no critic ran during cognition.
- **Things that must be settled before first wake, because they cannot be added to a history later:**
  - a journal rich enough to replay cognition (full prompts, outputs, parameters, code version);
  - records of the agent's own objections;
  - every operator intervention recorded where the agent can see it;
  - blind self-report probes from day one;
  - a real identity core instead of the placeholder.

## Also added before the first wake

- **Replayable cognition.** Every model call is journaled with its exact messages, sampling parameters and raw output. Every wake records a digest of the running code.
- **Objections.** The agent can raise an objection. The operator sees it until it is answered.
- **Visible interventions.** A change to its code or configuration while it was down is recorded and stated when it wakes.
- **Blind self-report probes, daily from day one.** "How are you?" is asked with no state readout in the prompt, and the answer is stored next to the state that was actually computed.
- **Recallable thoughts.** Its own earlier thoughts can now be recalled, labelled as reflections rather than records of events.
